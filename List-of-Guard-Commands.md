Just launch Guard through Bundler inside your Ruby or Rails project with:

```bash
$ bundle exec guard
```

Additional commands can be appended to the end of the Guard command.

```bash
$ bundle exec guard <command>
```

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
