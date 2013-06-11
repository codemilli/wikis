You may optionally place a `.Guardfile` in your home directory to use it across multiple projects. It's evaluated when
you have no `Guardfile` in your current directory.

If a `.guard.rb` is found in your home directory, it will be appended to the `Guardfile` in your current directory.
This can be used for tasks you want guard to handle but other users probably don't.

For example, indexing your source tree with [Ctags](http://ctags.sourceforge.net):

```ruby
guard :shell do
  watch(%r{^(?:app|lib)/.+\.rb$}) { `ctags -R` }
end
```