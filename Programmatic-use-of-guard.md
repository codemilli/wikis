You can pass a `Guardfile` content or a `Guardfile` location progammatically when calling `Guard.setup`. Available options are as follow:

* `:guardfile`          - The path to a valid `Guardfile`.
* `:guardfile_contents` - A string representing the content of a valid `Guardfile`.

Remember, without any options given, Guard will look for a `Guardfile` in your current directory and if it does not find one, it will look for it in your `$HOME` directory.

`Guard.run_all` can be used to run all Guard plugins. You can pass a scope to it with the `:plugins` / `:plugin` or `:groups` / `:group` options. Run Guard plugins, e.g. from a Rakefile:

```ruby
require 'guard'
# You can omit the call to Guard.setup, Guard.run_all will call Guard.setup
# under the hood if Guard has not been setuped yet
Guard.run_all group: :features

# or with multiple groups
Guard.run_all groups: [:features, :documentation]
```

Specify a custom `Guardfile` path:

```ruby
require 'guard'

Guard.setup(guardfile: '/path/to/Guardfile')
```

Start Guard and with a `Guardfile` as a string:

```ruby
require 'guard'

guardfile = <<-EOF
  guard 'rspec' do
    watch(%r{^spec/.+_spec\.rb$})
  end
EOF

# You can omit the call to Guard.setup, Guard.start will call Guard.setup
# under the hood if Guard has not been setuped yet
Guard.start(guardfile_contents: guardfile)
```