## Hooks

Guard has a hook mechanism that allows you to insert callbacks for individual Guards. By default, each of the Guard instance methods has a **"_begin"** and an **"_end"** hook. For example, the `Guard::Guard#start` method has a _:start_begin_ hook that is run immediately before `Guard::Guard#start` and a _:start_end_ hook that is run immediately after `Guard::Guard#start`.

## Callbacks

You can set your callback for a specific Guard in your Guardfile with the `Guard::DSL.callback` method. There are two ways to define your callbacks:

### With a block

The first argument to `Guard::Dsl#callback` is the hook of interest. The block contains the code to run. For example, to have Guard open TextMate when it first starts up:

```ruby
# Guardfile
guard 'rspec' do
  watch(...) { ... }

  callback(:start_begin) { `mate .` }
end
```

### Without a block

If you have more complex code to run, you can create a separate object to contain that code. In order for the callback to run, it must have a `#call` (or `.call` if it's a module) method that receives the class of the Guard associated with the callback, the hook event, and a splat of other arguments. For `Guard::Dsl#callback`, you pass the object (or the module) and the hook(s) you are interested in. Here is an example of a Timer plugin.

```ruby
# Guardfile
class Guard::Timer
  def times
    @times ||= Hash.new({})
  end

  def call(guard_class, event, *args)
    event.to_s =~ /(.*)_(begin|end)/
    times[$1][$2] = Time.now
    puts "#{guard_class} received these args: #{args} for #{event}"

    if $2 == 'end'
      time = times[$1]['end'] - times[$1]['begin']
      puts "#{guard_class} took #{time} seconds to run"
    end
  end
end

guard 'rspec' do
  watch(...) { ... }

  callback(Timer.new, [:start_begin, :start_end])
end
```

For the default **"_begin"** hooks, the `*args` that are passed to `#call` are the matched files that Guard has detected changes on. For the default **"_end"** hooks, `*args` are the results of the Guard action that was executed.

## NOTES / Caveats

Currently, callbacks are fired only if the given plugin implements the related method, e.g. `Guard-Rspec` doesn't currently implement `stop`, so callbacks for `:stop_begin` and `:stop_end` won't be called. The quick workaround is to add these methods through monkey-patching, but of course, caution is advised when doing so:

```ruby
# Required for instance_methods to have actual methods
require 'guard/rspec'

module ::Guard
  class RSpec < Plugin
    # Always check in case a future version of the plugin
    # implements the method
    unless instance_methods.include?(:stop)
      def stop; end
    end
  end
end

guard 'rspec' do
  watch(...) { ... }
  callback(Foo.action, [:stop_begin, :stop_end]) # now works
end
```


## Developers

If you are developing a Guard and want end users or other gems to be able to hook into certain parts of your code, then you can create a custom hook with the `#hook` method. You define the hook's name with either a symbol or string. If passed a symbol, the hook name will be the name of the calling method with the symbol appended. If passed a string, the hook name will be the string.

```ruby
module Guard
  class MyGuard < Guard
    def start
      # some code
      hook :custom_hook_1  # this hook's name will be :start_custom_hook_l
      # more code
      hook "custom_hook_2"  # this hook's name will be :custom_hook_2
      # rest of code
    end
    # the default hooks :start_begin and :start_end will still be available
  end
end
```
