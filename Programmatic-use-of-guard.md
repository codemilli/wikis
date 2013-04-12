The Guardfile DSL can also be used in a programmatic fashion by calling
[Guard::Dsl.evaluate_guardfile](http://rubydoc.info/github/guard/guard/master/Guard/Dsl#evaluate_guardfile-class_method).

Available options are as follow:

* `:guardfile`          - The path to a valid `Guardfile`.
* `:guardfile_contents` - A string representing the content of a valid `Guardfile`.

Remember, without any options given, Guard will look for a `Guardfile` in your current directory and if it does not find
one, it will look for it in your `$HOME` directory.

The `Guard.setup` uses `evaluate_guardfile`, but does a little but more magic around it. 
It currently requires the options `plugin: [], group: []`. See [#423](https://github.com/guard/guard/issues/423).

`Guard.run_all` can be used to run guards. However, make sure to pass `Guard::Group` instances as shown in the following example (see [#420](https://github.com/guard/guard/issues/420)).

Run guards, e.g. from a Rakefile:

```ruby
require 'guard'
Guard.setup group: [], plugin: []
Guard.run_all group: Guard::Group.new(:features)
```

Evaluate a `Guardfile`:

```ruby
require 'guard'

Guard.setup
Guard.start(:guardfile => '/path/to/Guardfile')
```

Evaluate a string as `Guardfile`:

```ruby
require 'guard'

Guard.setup

guardfile = <<-EOF
  guard 'rspec' do
    watch(%r{^spec/.+_spec\.rb$})
  end
EOF

Guard.start(:guardfile_contents => guardfile)
```