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