
(This feature is in the "hook" branch as of April 30, 2011.)

## Hooks

Guard has a hook mechanism that allows you to insert callbacks for individual Guards. By default, each of the Guard instance methods has a "_begin" and an "_end" hook. For example, the <tt>#start</tt> method will have a :start_begin hook that is run immediately before <tt>#start</tt> and a :start_end hook that is run immediately after <tt>#start</tt>.

## Callbacks

You can set your callback for a specific Guard in your Guardfile with the <tt>DSL.callback</tt> method. There are two ways to define your callbacks:

### With A Block

The first argument to <tt>.callback</tt> is the hook of interest. The block contains the code to run. For example, to have Guard open TextMate when it first starts up:

```ruby
# Guardfile
guard 'rspec' do
  watch(...) { ... }

  callback(:start_end) { `mate .` }
end
```

### Without A Block

If you have more complex code to run, you can create a separate object to contain that code. In order for the callback to run, it must have a <tt>#call</tt> method that receives the class of the Guard associated with the callback, the hook event, and a splat of other arguments. For <tt>.callback</tt>, you pass the object and the hook(s) you are interested in. Here is an example of a Timer plugin.

```ruby
# Guardfile
class Guard::Timer
  def times
    @times ||= {}
  end

  def call(guard_class, event, *args)
    event.to_s =~ /(.*)_(begin|end)/
    times[[guard_class, $1, $2]] = Time.now
    puts "#{guard_class} received these args: #{args} for #{event}"

    if $2 == 'end'
      time = @times[[guard_class, $1, 'end']] - @times[[guard_class, $1, 'begin']]
      puts "#{guard_class} took #{time} seconds to run"
    end
  end
end

guard 'rspec' do
  watch(...) { ... }

  callback(Timer.new, [:start_begin, :start_end])
end
```

For the default "_begin" hooks, the <tt>*args</tt> that are passed to <tt>#call</tt> are the matched files that Guard has detected changes on. For the default "_end" hooks, <tt>*args</tt> are the results of the Guard action that was executed.

## Developers

If you are developing a Guard and want end users or other gems to be able to hook into certain parts of your code, then you can create a custom hook with the <tt>#hook</tt> method. You define the hook's name with either a symbol or string. If passed a symbol, the hook name will be the name of the calling method with the symbol appended. If passed a string, the hook name will be the string.

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
