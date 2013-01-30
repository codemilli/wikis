Pry allows you to create custom commands, so you can customize the Guard interactor. See https://github.com/pry/pry/wiki/Command-system and https://github.com/pry/pry/wiki/Custom-commands for more information.

## Switch RSpec formatter

This commands allows you to switch the used RSpec formatter quickly:

```ruby
Pry::Commands.block_command 'fuu', "Use fuubar formatter in rspec" do
  options = ::Guard.guards(:rspec).runner.options
  options[:cli] = options[:cli].sub(/\-\-format \w+/, '--format Fuubar')
  output.puts "Using Fuubar as RSpec formatter."
end

Pry::Commands.block_command 'doc', "Use documentation formatter in rspec" do
  options = ::Guard.guards(:rspec).runner.options
  options[:cli] = options[:cli].sub(/\-\-format \w+/, '--format documentation')
  output.puts "Using Documentation as RSpec formatter."
end
```

## Disable plugins unneeded for Guard interaction

`~/.guardrc` is just a [pryrc] that is specific to Guard, so you can use it to disable plugins only in Guard's Pry instance and not those you normally use in development. For instance, [pry-stack_explorer] is a useful plugin for debugging, but its state output such as frame number indication is unwanted noise in Guard output. So, in `~/.guardrc` simply disable it:

```ruby
Pry.plugins['stack_explorer'] && Pry.plugins['stack_explorer'].disable!
```

Note that rc files are evaluated *before* plugins are fully loaded.

[pryrc]: https://github.com/pry/pry/wiki/Pry-rc
[pry-stack_explorer]: https://github.com/pry/pry-stack_explorer