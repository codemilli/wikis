_This is a WIP, please not edit. Thanks, [@rymai](https://github.com/rymai)._

**Guard 2.0 comes with several API changes (the majority is backward-compatible, but not all).**

## Changes in `Guard`

### Method behavior changes

* `Guard.guards(filter = nil)` (deprecated below) / `Guard.plugins(filter = nil)`: the return value has changed: it returns a single `Plugin` if there's only one matching, or an array of `Plugin`s otherwise)
* `Guard.groups(filter = nil)`: the return value has changed: it returns a single `Group` if there's only one matching, or an array of `Group`s otherwise)

### Deprecated methods

* `Guard.guards(filter = nil)` is deprecated and replaced by `Guard.plugins(filter = nil)` (be careful, its return value has changed: it returns a single `Plugin` if there's only one matching, or an array of `Plugin`s otherwise)
* `Guard.add_guard(name, options = {})` is deprecated and replaced by `Guard.add_plugin(name, options = {})`
* `Guard.get_guard_class(name, fail_gracefully = false)` is deprecated and replaced by `Guard::PluginUtil.new(name).plugin_class(:fail_gracefully =>
      fail_gracefully)`
* `Guard.locate_guard(name)` is deprecated and replaced by `Guard::PluginUtil.new(name).plugin_location`
* `Guard.guard_gem_names` is deprecated and replaced by `Guard::PluginUtil.plugin_names`

## Changes in `Guard::Guard`

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
      # you can still access the watchers with options[:watchers]
      # rest of the implementation...
    end
  end
end
```

## Changes in `Guard::Dsl`

### Deprecated methods

* `Guard::Dsl.evaluate_guardfile(options)` is deprecated and replaced by `Guard::Guardfile::Evaluator.new(options).evaluate_guardfile`

## Changes in `Guard::Guardfile`

### Deprecated methods

* `Guard::Guardfile.create_guardfile(options)` is deprecated and replaced by `Guard::Guardfile::Generator.new(options).create_guardfile`
* `Guard::Guardfile.initialize_template(plugin_name)` is deprecated and replaced by `Guard::Guardfile::Generator.new.initialize_template(plugin_name)`
* `Guard::Guardfile.initialize_all_templates` is deprecated and replaced by `Guard::Guardfile::Generator.new.initialize_all_templates`

### Removed methods

* `Guard::Guardfile.duplicate_definitions?` has been removed and replaced by `Guard::Guardfile::Evaluator#guardfile_include?(plugin_name)`
