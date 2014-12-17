
### Guard Console

Guard shows a [Pry](http://pryrepl.org/) console whenever it has nothing to do and comes with some Guard specific Pry
commands:

 * `↩`, `a`, `all`: Run all plugins.
 * `h`, `help`: Show help for all interactor commands.
 * `c`, `change`: Trigger a file change.
 * `n`, `notification`: Toggles the notifications.
 * `p`, `pause`: Toggles the file listener.
 * `r`, `reload`: Reload all plugins.
 * `o`, `scope`: Scope Guard actions to plugins or groups.
 * `s`, `show`: Show all Guard plugins.
 * `e`, `exit`: Stop all plugins and quit Guard

The `all` and `reload` commands supports an optional scope, so you limit the Guard action to either a Guard plugin or
a Guard group like:

```bash
[1]  guard(main)> all rspec
[2]  guard(main)> all frontend
```

Remember, you can always use `help` on the Pry command line to see all available commands and `help <command>` for
more detailed information. `help guard` will show all Guard related commands available

Pry supports the Ruby built-in Readline, [rb-readline](https://github.com/luislavena/rb-readline) and
[Coolline](https://github.com/Mon-Ouie/coolline). Just install the readline implementation of your choice by adding it
to your `Gemfile`.

You can also disable the interactions completely by running Guard with the `--no-interactions` option.

### Customizations

Further Guard specific customizations can be made in `~/.guardrc` that will be evaluated prior the Pry session is
started (`~/.pryrc` is ignored). This allows you to make use of the Pry plugin architecture to provide custom commands
and extend Guard for your own needs and distribute as a gem. Please have a look at the
[Pry Wiki](https://github.com/pry/pry/wiki) for more information.

### Guard Signals

You can also interact with Guard by sending POSIX signals to the Guard process (all but Windows and JRuby).

If the Pry interactor is used, then `Ctrl-C` is delegated to Pry to exit continuation and `Ctrl-D` to exit Guard.
Without interactor, `Ctrl-C` exits Guard and `Ctrl-D` is ignored.

#### Pause watching

```bash
$ kill -USR1 <guard_pid>
```

#### Continue watching

```bash
$ kill -USR2 <guard_pid>
```