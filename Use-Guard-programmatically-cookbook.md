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

    # With Guard 0.8.0+ this will find the first defined 'less' guard:
    Guard.guards('less').run_all
    # If you're stuck on an older version for some reason, you can find manually:
    less = Guard.guards.select { |g| g.is_a? Guard::Less }.first
    less.run_all
  end
end
```

See [ticket #121](https://github.com/guard/guard/issues/121) for additional details.

If you want to do something like this in a Capistrano task run remotely, remember that you may need to include Guard and the needed plugins in a Bundler group other than development in your `Gemfile`.

### Use Guard from a simple Ruby script

In case you can't or don't want to use a Rake task, it's also possible to invoke Guard from a simple script file – which you can run using `bundle exec ruby myscript.rb` from the Terminal console.

```ruby
require 'rubygems'
require 'bundler/setup'

require 'guard'
require 'rake'

# Optional: If you use Guard::Rake you also have to manually start up Rake to be able to process the Rakefile
rake = Rake::Application.new
Rake.application = rake
rake.init
rake.load_rakefile

# Let's load Guard and process the Guardfile
Guard.setup
Guard::Dsl.evaluate_guardfile(:guardfile => 'Guardfile')

# Finally run all Guards
Guard.run_all({})
```
