Just launch Guard through Bundler inside your Ruby or Rails project with:

```bash
$ bundle exec guard
```

Additional commands can be appended to the end of the Guard command.

```bash
$ bundle exec guard <command>
```

### Commands

* [Init](#init) - setup a new Guardfile with default plugin config templates
* [Help](#help) - show detailed help for other commands
* [List](#list) - show available and used plugins
* [Show](#show) - show configuration options for each used plugin
* [Notifiers](#notifiers) - show list of available notifiers and which ones are used


### Init
You can generate a Guardfile and have all installed plugins be automatically added into
it by running the `init` task without any option:

```bash
$ bundle exec guard init
```

You can also specify the name of an installed plugin to only get that plugin template
in the generated Guardfile:

```bash
$ bundle exec guard init <guard-name>
```

You can also specify the names of multiple plugins to only get those plugin templates
in the generated Guardfile:

```bash
$ bundle exec guard init <guard1-name> <guard2-name>
```

You can also define your own templates in `~/.guard/templates/` which can be appended in the same way to your existing
`Guardfile`:

```bash
$ bundle exec guard init <template-name>
```

**Note**: If you already have a `Guardfile` in the current directory, the `init` task can be used
to append a supplied template from an installed plugin to your existing `Guardfile`.

You also can generate an empty `Guardfile` by running the `init` task with the bare 
option: (`-b`/`--bare`)

```bash
$ bundle exec guard init --bare
$ bundle exec guard init -b # shortcut
```

### Help

You can always get help on the available tasks with the `help` task:

```bash
$ bundle exec guard help
```

Requesting more detailed help on a specific task is simple: just append the task name to the help task.
For example, to get help for the `start` task, simply run:

```bash
$ bundle exec guard help start
```

### List

You can list the available plugins with the `list` task:

```bash
$ bundle exec guard list
+----------+--------------+
| Plugin   | In Guardfile |
+----------+--------------+
| Compass  | ✘            |
| Cucumber | ✘            |
| Jammit   | ✘            |
| Ronn     | ✔            |
| Rspec    | ✔            |
| Spork    | ✘            |
| Yard     | ✘            |
+----------+--------------+
```

### Show

You can show the structure of the groups and their plugins with the `show` task:

```bash
$ bundle exec guard show
+---------+--------+-----------------+----------------------------+
| Group   | Plugin | Option          | Value                      |
+---------+--------+-----------------+----------------------------+
| Specs   | Rspec  | all_after_pass  | true                       |
|         |        | all_on_start    | true                       |
|         |        | cli             | "--fail-fast --format doc" |
|         |        | focus_on_failed | false                      |
|         |        | keep_failed     | true                       |
|         |        | run_all         | {}                         |
|         |        | spec_paths      | ["spec"]                   |
+---------+--------+-----------------+----------------------------+
| Docs    | Ronn   |                 |                            |
+---------+--------+-----------------+----------------------------+
```

This shows the internal structure of the evaluated `Guardfile` or `.Guardfile`, with the `.guard.rb` file. You can
read more about these files in the [shared configuration section](https://github.com/guard/guard/wiki/Shared-configurations).

### Notifiers

You can show the notifiers, their availablity and options with the `notifier` task:

```bash
$ bundle exec guard notifiers
+-------------------+-----------+------+------------------------+-------------------+
| Name              | Available | Used | Option                 | Value             |
+-------------------+-----------+------+------------------------+-------------------+
| gntp              | ✔         | ✘    | sticky                 | false             |
+-------------------+-----------+------+------------------------+-------------------+
| growl             | ✘         | ✘    | sticky                 | false             |
|                   |           |      | priority               | 0                 |
+-------------------+-----------+------+------------------------+-------------------+
```

This shows if a notifier is available on the current system, if it's being used and the
current options (which reflects your custom options merged into the default options).
