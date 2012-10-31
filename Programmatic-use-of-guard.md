The Guardfile DSL can also be used in a programmatic fashion by calling
[Guard::Dsl.evaluate_guardfile](http://rubydoc.info/github/guard/guard/master/Guard/Dsl#evaluate_guardfile-class_method).

Available options are as follow:

* `:guardfile`          - The path to a valid `Guardfile`.
* `:guardfile_contents` - A string representing the content of a valid `Guardfile`.

Remember, without any options given, Guard will look for a `Guardfile` in your current directory and if it does not find
one, it will look for it in your `$HOME` directory.

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
