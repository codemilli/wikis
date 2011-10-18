The flexibility of Guard allows for some creative uses beyond simply running tests, etc. If you've come up with interesting atypical use cases or useful code snippets, please share them here!

### Use guard programmatically in a Rake (or Capistrano) task

Perhaps you wish to compile asset files from CoffeeScript, LESS, SCSS or the like on-demand without starting Guard in a long-running fashion. You may be prototyping an early-stage app and want to precompile these assets and rsync everything straight to a server, or you're simply using some other custom strategy of deploying assets where you want control of when and how this is done. In that case, you might want a Rake or Capistrano task for the job, and why duplicate the effort to specify where the source files are, where the built ones should go, and how to build them if you already have a Guard plugin configured to do so? Here's an example of using Guard programmatically in a Rake task to compile LESS to CSS:

```ruby
require 'guard'

namespace :assets do
  desc 'Generate CSS from all source LESS files'
  task :less do
    Guard.setup
    Guard::Dsl.evaluate_guardfile(:guardfile => 'Guardfile', :group => ['frontend'])

    # Guard will hopefully have a nicer way of getting at your guards:
    less = Guard.guards.select { |g| g.is_a? Guard::Less }.first
    less.run_all
  end
end
```

If you want to do something like this in a Capistrano task run remotely, remember that you may need to include Guard and the needed plugins in a Bundler group other than development in your `Gemfile`.

### Only use guard's listener notifications

It may make sense for you to write your own listener loops. For example, you might want to call a specific method when a file changes. To do that, you don't need a Guardfile at all, you could simply use `Guard::Listener` like this:

```ruby
listener = Guard::Listener.select_and_init # selects an OS-specific listener
listener.on_change do |files|              # sets a callback to be invoked whenever a file is changed
  # do stuff with the files
end
listener.start                             # starts the event loop
```

This will require you to do your own filtering, but it gives you the freedom to do whatever you want with the files.
