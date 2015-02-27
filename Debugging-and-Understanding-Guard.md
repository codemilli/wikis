## Intro

Guard's syntax and behavior tend to be *very* confusing to newcomers.

This will hopefully be changed in the near future.

Meanwhile, we hope this guide will help you quickly "get it", without having to go through hours of mind-bending "mistakes".

If you don't take a few minutes to even just skim through this, you might get stuck for hours trying to even get `Guard` doing something simple.

But, if you do ... you'll be able to force `Guard` to do truly awesome things - that we as `Guard` authors and maintainers would have *never* imagined!.

(Do share with us if you create something cool! Feel free to even add a Wiki page about it!)


## Confusing Simple Example

Even this trivial example is misleading:

```ruby
guard :bundler do
  watch('Gemfile')
end
```

`watch` does not mean Guard will `watch` the file.

Nope.

It means: "when `Gemfile` is DETECTED as changed, added or removed, let this plugin handle it.

For the above code to "work as expected",

1. Guard has to be ALREADY watching the directory the `Gemfile` is in (although this is platform/adapter specific).
2. The plugin has be designed to respond to the *kind* of change (modified *or* added *or* deleted)
3. The plugin has to be designed to actually handle that file (and not ignore the change)

Well, if it "doesn't work", how do you know what's wrong then?

## Debugging

Let's dive into debugging, because *this* will save you *tons* of hours:

### Is the file passed to the plugin?

First, run guard with the `-d` parameter (`bundle exec guard -d`)

Now, if you change the file while running Guard, you should see:

```
20:43:26 - DEBUG - Interactor was stopped or killed
20:43:26 - DEBUG - Hook :run_on_modifications_begin executed for Guard::Bundler
20:43:26 - DEBUG - Hook :run_on_modifications_end executed for Guard::Bundler
20:43:26 - DEBUG - Start interactor
```

This says a few things:

1. That Guard detected *relevant* changes (meaning - one of the plugins matched the changes)
2. That *some* change matching the `watch` statement was passed to the plugin
3. That the change was a file `modification`
4. That the plugin actually handles modified files

So if nothing is happening at this point, check that:
1. The plugin is configured properly
2. The plugin doesn't actually ignore the file you are watching

First, let's start with plugin problems (and then we'll get back to Guard).

### Here's a incorrect example:

```ruby
guard :minitest, options do
  watch('project/module/foo.rb')
end
```

And here's the debug output when editing e.g. `project/module/foo.rb`:

```
20:43:26 - DEBUG - Hook :run_on_additions_begin executed for Guard::Minitest
20:43:26 - DEBUG - Hook :run_on_additions_end executed for Guard::Minitest
```

This means `:minitest` *got* the change, but *didn't do anything*.

Why? Because minitest responds to *test files*.

So, if minitest gets "foo.rb", it will do *nothing* by design.
But if you pass "foo_test.rb" (given that file exists), it will run the tests.

If we did something silly like passing `Gemfile` to `Guard::Minitest`, it wouldn't anything either.

### So, how do you fix it?

Well, in this case if we want `Guard::Minitest` to run the tests in `foo_test.rb`, we have to map the files ourselves, e.g:

```ruby
guard :minitest, options do
  watch('project/module/foo.rb') { 'project/tests/module/foo_test.rb' }
end
```

Here's how to read this: "if Guard detects changes in `project/module/foo.rb`, it will pass `project/module/foo_test.rb` to Guard::Minitest.

Without the block, it would pass `project/module/foo.rb`, which Guard::Minitest just ignores.

### What's the best thing to try out first?

Ideally, rename your `Guardfile`, update your gems, and run `bundle exec guard init` again - and tweak the defaults just enough to get things working.

If you think the defaults could be better, submit an issues to the plugin home page (which you can usually in the gem's README or here: https://rubygems.org/gems or on GitHub). Chances are, the plugin might have a fork here in this GitHub organization: https://github.com/guard. If no one is responding, just mention me in the comments (as `@e2`).

### Debugging the matchers in Guard

If the plugin is *not* getting the event - there are a few tricks to work out why.

With `bundle exec guard init minitest` for the example above, the `Guardfile` will include something like:

```ruby
guard :minitest do
  # This runs the modified test
  watch(%r{^test/(.*)\/?test_(.*)\.rb$})

  # This calls the plugin with a new file name - which may not even exist
  watch(%r{^lib/(.*/)?([^/]+)\.rb$})     { |m| "test/#{m[1]}test_#{m[2]}.rb" }

  # This call the plugin with the 'test' parameter - see Guard::Minitest docs
  # for information in how it finds/choose files in the given 'test' directory
  watch(%r{^test/test_helper\.rb$})      { 'test' }
end
```

The "easy" way to see if a watch is triggered is to just print it, e.g:

```ruby
guard :minitest do
  watch(%r{^lib/(.*/)?([^/]+)\.rb$}) do |m|
    "test/#{m[1]}test_#{m[2]}.rb".tap do |result|
      Guard::UI.info "Sending changes to Minitest: #{result.inspect}"
      Guard::UI.info "The original match is: #{m.inspect}"
    end
  end
end
```

(Note the `tap` there).

If you are not getting the output, try restarting Guard - especially since newer version of Guard may not reload themselves.


### Another bad example

Guard shell had a bad design decision, but quickly became too popular to change things.

```ruby
guard :shell do
  watch /(.*)/ do |m|
    `echo #{m[0]}`
  end
end
```

This is a bit confusing, because while it works as expected, it's not how it "should" work.

The Guard::Shell plugin just prints the stuff returned by the block.

The "Guard way" of doing things would be to either have something like:

```ruby
# this non-existing plugin would print whatever is returned
guard :print, output: $stdout do
  watch /(.*)/ do |m|
    `echo #{m[0]}`
  end
end
```

(NOTE: this plugin doesn't exist - it's just an example)

or:

```ruby
# this non-existing plugin would e.g. pass the string to a system() call
guard :execute, any_return: true do
  watch /(.*)/ do |m|
    'echo #{m[0]}'
  end
end
```

(NOTE: this plugin also doesn't exist - it's just an example)

or even:

```ruby
# this non-existing plugin would e.g. capture exceptions and throw :task_failed on errors
guard :call_safely, any_return: true do
  watch /(.*)/ do |m|
    Proc.new do
     system("my_tool #{m[1]}") || fail "Command failed: #{m[1]}"
    end
  end
end
```

This is because `Guard` expects you to return paths (unless you provide the `any_return` option).

And `Guard` expects your `watch` block to just work out which paths to pass to the plugin.

Also, `Guard` expects failing tasks to throw the `:task_failed` symbol - no
gracefully notify Guard that the failure is a normal one to occur (e.g. failing test).


### Debugging complex rules

If you have complex rules, and the file you're changing is triggering the wrong actions ...

... this should help show you how Guard matches changes and what it calls the plugin.

Start `Guard` and in the `Pry` session type in:

```ruby
# NOTE: this API is somewhat internal and in progress of being defined
plugin = Guard.state.session.plugins.all(:minitest).first

Guard::Watcher.match_files(plugin, %w(project/module/foo.rb))
```

Or, on older versions of `Guard`:

```ruby
plugin = Guard.plugin(:minitest)
Guard::Watcher.match_files(plugin, %w(project/module/foo.rb))
```

This will show you what your rules are returning.

One handy option is `:first_match`, e.g.:

```ruby
guard :minitest, first_match: true do
  # Rule for all tests
  watch(/test\/(.*)_test\.rb$/)  # no block means return the matched file

  # Run multiple tests when an abstract base class changes:
  watch(/lib\/net/base.rb$/) { |m| "tests/network" }

  # Special rule for files in `ui` directory
  watch(/lib\/ui\/(.*)\.rb$/) { |m| "acceptance/#{m[1]}_test.rb" }

  # General translating implementation files to test files
  watch(/lib\/(.*)\.rb$/) { |m| "tests/#{m[1]}_test.rb" }

  # Note the `nil` at the end to avoid passing file to plugin
  watch(/(.*)/) { |m| Guard::UI.puts "Unknown file: #{m[1]}"; nil }
end
```

The `first_match` prevents `Guard` for running the plugin multiple times for every block the changed (or added, or removed) file matches.

### When Guard is not responding to changes

How do you know if `Guard` is even responding to changes?

Well, when running guard in debug mode with `-w`, you'll know by:

```
20:43:26 - DEBUG - Interactor was stopped or killed
20:43:26 - DEBUG - Start interactor
```

The Interactor is `killed` whenever a file change is *relevant* - meaning it matches *any* `watch` rule in *any* plugin.

'Start interactor' means `Guard` is finished processing all the changes.

So if you don't see those lines, it means `Guard` didn't get *any* changes.

### Global watch trick

You can put a 'catch all' block at the top of your `Guard`, and it will go into the default group:

```ruby
watch(/(.*)/) { |m| Guard::UI.puts "Unknown file: #{m[1]}"; nil }
```

If you see the message (or the debug statement above), you'll know `Guard` is watching the file.

### "Ok, Guard is still not watching the file. What do I do?"

If you're using an editor, try changing the file using a tool that doesn't make backups or use `atomic save` (like most editors do), e.g.

```bash
$ touch test/foo_test.rb
```

If that triggers a change, but your editor doesn't, go here to `Listen` Wiki here, to work out the problem: https://github.com/guard/listen/wiki (in short, try disabling `atomic` save in your editor, or try tweaking file save backup options in your editor).

### "Ok, I tried `touch` - didn't work"

This may be a problem in either `Guard` or [Listen](https://github.com/guard/listen).

If you suspect `Guard` is the problem (because modifying other files in other directories triggers changes), check the following:

1. If you're on Linux, check if the file is a symlink (also, try running guard with the `-p` option to see if there's a difference)
2. Work out the *real* directory containing the *real* file

If the file is a symlink, check where it's symlinked to - then not which directory it *really* is in.

Then, make sure *that* directory is watched:

In Guard's Pry session, type in:

```ruby
Guard.state.session.watchdirs
```

Or, in older versions of `Guard`:

```
# Should work, but I'm not sure
Guard.instance_variable_get(:@watchdirs)
```

Make sure the directory is *physically* in one of those directories.

(You can change this setting using the `-w` parameter in the commandline, or by using the `directories` statement in your `Guardfile`)

Guard watches directories recursively, so watching the parent directory should be enough.

Also, make sure you're not using `chdir` anywhere - because this may confuse `Guard`.

### "Nope, watched dirs are fine and I still don't see any changes"

Then, your file may be ignored with the ignore rules. But it's best to check this from Listen:

```
$ LISTEN_GEM_DEBUGGING=1 bundle exec guard -d
```

If you don't understand the output (clue: the `final changes` should show what Guard is getting), then go through the Listen Wiki for more info: https://github.com/guard/listen/wiki

### "I'm still stuck"

If you are getting "nothing" or "too many changes", here's how to get an answer quickly:

1. include your `Guardfile` (mostly the rules)
2. include your output from running `Guard` with the `-d` flag (if it's long, put it into a Gist)
2. include the output using `LISTEN_GEM_DEBUGGING=1` above or even `LISTEN_GEM_DEBUGGING=2` by pasting the output into a Gist

Those 3 should be enough for us to help you work out the problem.


### Summary

At this point you should be a master at Guard - enough to know when something is problem with your config or with Guard.

Please report bugs as soon as possible (with the above info if you think the cause isn't "obvious").

Feel free to create Pull Requests - though to save time, open an issue first and ask to get guidance (since Guard is undergoing heavy rework).

Also, feel free to ask for new features or improvements - since Guard 3.x may be soon released with any wishes you have.

And, feel free to update/correct this Wiki to help others.

Thanks and have a great time using Guard!
