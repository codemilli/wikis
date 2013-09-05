_This is a WIP, please not edit. Thanks, [@rymai](https://github.com/rymai)._

**Guard 2.0 comes with several API changes (the majority is backward-compatible, but not all).**

### `Guard::Guard` deprecated in favor of `Guard::Plugin`

To remove the confusion between Guard and its many plugins (guard-rspec, guard-pow, guard-livereload etc.), `Guard::Guard` is renamed `Guard::Plugin`. `Guard::Guard` is deprecated so if you're a plugin maintainer, in your next (major) release **that will depend on Guard ~> 2.0** you must make your plugin inherit from `Guard::Plugin` instead of `Guard::Guard`.

Also, please be sure to change the `#initialize` signature from `#initialize(watchers = [], options = {})` to `#initialize(options = {})` (watchers are now passed in the `options` argument directly).

For instance, for guard-rspec:
```ruby
module Guard
  class RSpec < Guard
    def initialize(watchers = [], options = {})
      super
      # rest of the implementation...
    end
  end
end
```

should become:

```ruby
module Guard
  class Bundler < Plugin
    def initialize(options = {})
      super
      # rest of the implementation...
    end
  end
end
```