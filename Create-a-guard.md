Creating a new Guard is very easy. For example, to create a Guard named `yoyo` just create a new gem by running `bundle gem guard-yoyo`. Please make your Guard start with `guard-`, so that it can easily be found on RubyGems.

```bash
$ bundle gem guard-yoyo
$ cd guard-yoyo
```

Now extend the project structure to have an initial Guard:

```bash
.travis.yml  # bonus point!
CHANGELOG.md # bonus point!
Gemfile
guard-yoyo.gemspec
Guardfile
lib/
  guard/
    yoyo/
      templates/
        Guardfile # needed for `guard init <guard-name>`
      version.rb
    yoyo.rb
test/ # or spec/
README.md
```

Your Guard main class `Guard::Yoyo` in `lib/guard/guard-yoyo.rb` must inherit from
[Guard::Guard](http://rubydoc.info/github/guard/guard/master/Guard/Guard) and should overwrite at least the
`#run_on_change` task methods.

Here is an example scaffold for `lib/guard/yoyo.rb`:

```ruby
require 'guard'
require 'guard/guard'

module Guard
  class Yoyo < Guard

    # Initializes a Guard plugin.
    # Don't do any work here, especially as Guard plugins get initialized even if they are not in an active group!
    #
    # @param [Array<Guard::Watcher>] watchers the Guard plugin file watchers
    # @param [Hash] options the custom Guard plugin options
    # @option options [Symbol] group the group this Guard plugin belongs to
    # @option options [Boolean] any_return allow any object to be returned from a watcher
    #
    def initialize(watchers = [], options = {})
      super
    end

    # Called once when Guard starts. Please override initialize method to init stuff.
    #
    # @raise [:task_has_failed] when start has failed
    # @return [Object] the task result
    #
    def start
    end

    # Called when `stop|quit|exit|s|q|e + enter` is pressed (when Guard quits).
    #
    # @raise [:task_has_failed] when stop has failed
    # @return [Object] the task result
    #
    def stop
    end

    # Called when `reload|r|z + enter` is pressed.
    # This method should be mainly used for "reload" (really!) actions like reloading passenger/spork/bundler/...
    #
    # @raise [:task_has_failed] when reload has failed
    # @return [Object] the task result
    #
    def reload
    end

    # Called when just `enter` is pressed
    # This method should be principally used for long action like running all specs/tests/...
    #
    # @raise [:task_has_failed] when run_all has failed
    # @return [Object] the task result
    #
    def run_all
    end

    # Default behaviour on file(s) changes that the Guard plugin watches.
    # @param [Array<String>] paths the changes files or paths
    # @raise [:task_has_failed] when run_on_change has failed
    # @return [Object] the task result
    #
    def run_on_changes(paths)
    end

    # Called on file(s) additions that the Guard plugin watches.
    #
    # @param [Array<String>] paths the changes files or paths
    # @raise [:task_has_failed] when run_on_additions has failed
    # @return [Object] the task result
    #
    def run_on_additions(paths)
    end

    # Called on file(s) modifications that the Guard plugin watches.
    #
    # @param [Array<String>] paths the changes files or paths
    # @raise [:task_has_failed] when run_on_modifications has failed
    # @return [Object] the task result
    #
    def run_on_modifications(paths)
    end

    # Called on file(s) removals that the Guard plugin watches.
    #
    # @param [Array<String>] paths the changes files or paths
    # @raise [:task_has_failed] when run_on_removals has failed
    # @return [Object] the task result
    #
    def run_on_removals(paths)
    end

  end
end
```

Please take a look at the source code of some of the [existing Guards](https://github.com/guard)
for more concrete example and inspiration.

## Inline Guard

Alternatively, a new Guard can be added inline to a `Guardfile` with this basic structure:

```ruby
require 'guard/guard'

module ::Guard
  class InlineGuard < ::Guard::Guard
    def run_all
    end

    def run_on_changes(paths)
    end
  end
end
```

[@avdi](https://github.com/avdi) has a very cool inline Guard example in his blog post
[A Guardfile for Redis](http://avdi.org/devblog/2011/06/15/a-guardfile-for-redis).