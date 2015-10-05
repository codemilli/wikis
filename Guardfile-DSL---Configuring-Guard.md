The Guardfile DSL is evaluated as plain Ruby, so you can use normal Ruby code in your `Guardfile` (and your `~/.guard.rb` file which is evaluated first if it exists).  

Guard itself provides the following DSL methods that can be used for configuration:

### Contents:

* [guard](#guard) - to define and configure plugins
* [watch](#watch) - to setup patterns matching relevant files
* [group](#group) - to organize plugins into groups
* [scope](#scope) - to set the default groups or plugins to activate
* [directories](#directories) - to tell Guard which directories to watch
* [clearing](#clearing) - whether Guard should clear the screen
* [notification](#notification) - whether Guard should use notifications (popups, etc.)
* [interactor](#interactor) - whether guard should start the Pry console
* [callback](#callback) - to setup extra actions inside hooks for a plugin
* [ignore](#ignore) - to ignore changes to irrelevant files
* [filter](#filter) - to ignore changes to irrelevant files
* [logger](#logger) - to enable/configure the logger

### guard

The `guard` method allows you to add a Guard plugin to your toolchain and configure it by passing the
options after the name of the plugin:

```ruby
guard :coffeescript, input: 'coffeescripts', output: 'javascripts'
```

You can define the same plugin more than once:

```ruby
guard :coffeescript, input: 'coffeescripts', output: 'javascripts'
guard :coffeescript, input: 'specs', output: 'specs'
```

### watch

~~The `watch` method allows you to define which files are watched by a Guard~~

The `watch` method tells Guard which changed files the plugin should respond to:

```ruby
guard :bundler do
  watch('Gemfile')
end
```

This means: *"out of all the files that get modified, added and removed, only let the file `Gemfile` (all file paths are relative to the current directory) be handled by this plugin ('bundler' in this case)"*.

String watch patterns are matched with [String#==](http://www.ruby-doc.org/core-1.9.3/String.html#method-i-3D-3D).
You can also pass a regular expression to the watch method:

```ruby
guard :jessie do
  watch(%r{^spec/.+(_spec|Spec)\.(js|coffee)})
end
```

This instructs the jessie plugin to watch for file changes in the `spec` folder,
but only for file names that ends with `_spec` or `Spec` and have a file type of `js` or `coffee`.

You can easily test your watcher regular expressions with [Rubular](http://rubular.com/).

When you add a block to the watch expression, you can modify the file name that has been
detected before sending it to the plugin for processing:

```ruby
guard :rspec do
  watch(%r{^lib/(.+)\.rb$}) { |m| "spec/lib/#{m[1]}_spec.rb" }
end
```

In this example the regular expression capture group `(.+)` is used to transform a file change
in the `lib` folder to its test case in the `spec` folder. Regular expression watch patterns
are matched with [Regexp#match](http://www.ruby-doc.org/core-1.9.3/Regexp.html#method-i-match).

You can also launch any arbitrary command in the supplied block:

```ruby
guard :shell do
  watch(/.*/) { `git status` }
end
```

*NOTE: Normally, most plugins expect the block to return a path or array of
paths - i.e. other plugins would think the `git status` output here is a
file path (which would cause an error), so this trick of returning the command
output only works for `guard-shell` plugin and other plugins that support
arbitrary results.*

You can also define `watch`es outside of a `guard` plugin. This is useful to
perform arbitrary Ruby logic (i.e. something project-specific).

```ruby
watch(/.*/) { |m| puts "#{m[0]} changed." }
```

### group

The `group` method allows you to group several plugins together. This comes in handy especially when you
have a huge `Guardfile` and want to focus your development on a certain part.

```ruby
group :specs do
  guard :rspec do
    watch(%r{^spec/.+_spec\.rb$})
  end
end

group :docs do
  guard :ronn do
    watch(%r{^man/.+\.ronn?$})
  end
end
```

Groups can be nested, reopened and can take multiple names to assign its plugin to multiple groups:

```ruby
group :desktop do
  guard 'livereload' do
    watch(%r{desktop/.+\.html})
  end

  group :mobile do
    guard 'livereload' do
      watch(%r{mobile/.+\.html})
    end
  end
end

group :mobile, :desktop do
  guard 'livereload' do
    watch(%r{both/.+\.html})
  end
end
```

Groups to be run can be specified with the Guard DSL option `--group` (or `-g`):

```bash
$ bundle exec guard -g specs
```

Plugins that don't belong to a group are part of the `default` group.

Another neat use of groups is to group dependent plugins and stop processing if one fails. In order
to make this work, the group needs to have the `halt_on_fail` option enabled and the Guard plugin
needs to throw `:task_has_failed` to indicate that the action was not successful.

```ruby
group :specs, halt_on_fail: true do
  guard :rspec do
    watch(/.../)
  end

  guard :cucumber do
    watch(/.../)
  end
end
```

### scope

The `scope` method allows you to define the default plugin or group scope for Guard, if not
specified as command line option. Thus command line group and plugin scope takes precedence over
the DSL scope configuration.

You can define either a single plugin or group:

```ruby
scope plugin: :rspec
scope group: :docs
```

or specify multiple plugins or groups.

```ruby
scope plugins: [:test, :jasmine]
scope groups: [:docs, :frontend]
```

If you define both the plugin and group scope, the plugin scope has precedence. If you use both the
plural and the singular option, the plural has precedence.

**Please be sure to call the `scope` method after you've declared your Guard plugins!**

### directories

This option limits the directories watch to those given, which can improve
responsiveness, performance and help reduce resource usage (CPU, memory) on
larger projects.

```ruby
directories %w(app config lib spec features)
```

Note: The `--watchdir` option overrides this. (see `--watchdir` above for extra
info).

Note: Since recursion cannot be disabled on OSX, all other backends were made
recursive - so if you want to watch selected directories AND files in the root
directory of your project, move them to another directory and create symlinks
back, e.g.

```
mkdir config
mv Gemfile config
ln -s config/Gemfile Gemfile
```

### clearing

Guard can clear the screen before every action (which some people prefer).

The this clearing behavior can be set to `:on` or `:off`:

```ruby
clearing :on
```

*NOTE: since clearing is more of a user setting, it's best to have each team member set this in their own `~/.guard.rb` file (instead of the project `Guardfile`).*

### notification

If you don't specify any notification configuration in your `Guardfile`, Guard goes through the list of available
notifiers and enables all that are available. If you specify your preferred library, auto detection will not take
place:

```ruby
notification :growl
```

will select the `growl` gem for notifications. You can also set options for a notifier:

```ruby
notification :growl, sticky: true
```

Each notifier has a slightly different set of supported options:

```ruby
notification :growl, sticky: true, host: '192.168.1.5', password: 'secret'
notification :gntp, sticky: true, host: '192.168.1.5', password: 'secret'
notification :libnotify, timeout: 5, transient: true, append: false, urgency: :critical
notification :notifu, time: 5, nosound: true, xp: true
notification :emacs
```

It's possible to use more than one notifier. This allows you to configure different notifiers for different OS if your
project is developed cross-platform or if you like to have local and remote notifications.

Notifications can also be turned off in the `Guardfile`, in addition to setting the environment variable `GUARD_NOTIFY`
or using the cli switch `-n`:

```ruby
notification :off
```

*NOTE: since notification is more of a user setting, it's best to have each team member set this in their own `~/.guard.rb` file (instead of the project `Guardfile`).*


### interactor

You can customize the Pry interactor history and RC file like:

```ruby
interactor guard_rc: '~/.my_guard-rc', history_file: '~/.my_guard_history_file'
```

If you do not need the Pry interactions with Guard at all, you can turn it off:

```ruby
interactor :off
```

### callback

The `callback` method allows you to execute arbitrary code before or after any of the `start`, `stop`, `reload`,
`run_all`, `run_on_changes`, `run_on_additions`, `run_on_modifications` and `run_on_removals` Guard plugins method.
You can even insert more hooks inside these methods.

```ruby
guard :rspec do
  watch(%r{^spec/.+_spec\.rb$})

  callback(:start_begin) { `mate .` }
end
```

Please see the [hooks and callbacks](https://github.com/guard/guard/wiki/Hooks-and-callbacks) page in the Guard wiki for
more details.

### ignore

The `ignore` method can be used to exclude files and directories from the set of files being watched. Let's say you have
used the `watch` method to monitor a directory, but you are not interested in changes happening to images, you could use
the ignore method to exclude them.

This comes in handy when you have large amounts of non-source data in you project. By default
[`.rbx`, `.bundle`, `.DS_Store`, `.git`, `.hg` ,`.svn`, `bundle`, `log`, `tmp`, `vendor/bundle`](https://github.com/guard/listen/blob/master/lib/listen/silencer.rb#L5-L9)
are ignored.

*NOTE: this option mostly helps when irrelevant changes are triggering guard tasks (e.g. a task starts before the editor finished saving all the files). Also, while it can reduce CPU time and increase responsiveness when using polling, instead, using `--watchdirs` is recommended for such "tuning" (e.g. large projects)*

Please note that method only accept regexps. See [Listen README](https://github.com/guard/listen#ignore--ignore).

To append to the default ignored files and directories, use the `ignore` method:

```ruby
ignore %r{^ignored/path/}, /public/
```

To _replace_ any existing ignored files and directories, use the `ignore!` method:

```ruby
ignore! /data/
```

### filter

Alias of the [ignore](https://github.com/guard/guard#ignore) method.

### logger

The `logger` method allows you to customize the [Lumberjack](https://github.com/bdurand/lumberjack) log output to your
needs by specifying one or more options like:

```ruby
logger level:       :warn,
       template:    '[:severity - :time - :progname] :message',
       time_format: 'at %I:%M%p',
       only:        [:rspec, :jasmine, 'coffeescript'],
       except:      :jammit,
       device:      'guard.log'
```

Log `:level` option must be either `:debug`, `:info`, `:warn` or `:error`. If Guard is started in debug mode, the log
level will be automatically set to `:debug`.

The `:template` option is a string which can have one or more of the following placeholders: `:time`, `:severity`,
`:progname`, `:pid`, `:unit_of_work_id` and `:message`. A unit of work is assigned for each action Guard performs on
multiple Guard plugin.

The `:time_format` option directives are the same as Time#strftime or can be `:milliseconds`

The `:only` and `:except` are either a string or a symbol, or an array of strings or symbols that matches the name of
the Guard plugin name that sends the log message. They cannot be specified at the same time.

By default the logger uses `$stderr` as device, but you can override this by supplying the `:device` option and set
either an IO stream or a filename.
