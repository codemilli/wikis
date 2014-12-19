
You can use additional command line options to enhance Guard. These can be appended to the command line:

```bash
$ bundle exec guard
```


#### `-c`/`--clear` option

The shell can be cleared after each change:

```bash
$ bundle exec guard --clear
$ bundle exec guard -c # shortcut
```

You may prefer to enable clearing in all projects by addin the `clearing`
statement (described below) in you `~/.guardrc` instead:

```ruby
clearing :on
```


#### `-n`/`--notify` option

System notifications can be disabled:

```bash
$ bundle exec guard --notify false
$ bundle exec guard -n f # shortcut
```

Notifications can also be disabled globally by setting a `GUARD_NOTIFY` environment variable to `false`.


#### `-g`/`--group` option

Scope Guard to certain plugin groups on start:

```bash
$ bundle exec guard --group group_name another_group_name
$ bundle exec guard -g group_name another_group_name # shortcut
```

See the Guardfile DSL below for creating groups.


#### `-P`/`--plugin` option

Scope Guard to certain plugins on start:

```bash
$ bundle exec guard --plugin plugin_name another_plugin_name
$ bundle exec guard -P plugin_name another_plugin_name # shortcut
```


#### `-d`/`--debug` option

Guard can display debug information (useful for plugin
developers) with:

```bash
$ bundle exec guard --debug
$ bundle exec guard -d # shortcut
```


#### `-w`/`--watchdir` option

Guard by default watches the current directory recursively, but you can tell Guard to watch only the directories you want:

```bash
$ bundle exec guard --watchdir source/files # watch a subdirectory of your project
$ bundle exec guard -w source/files # shortcut
$ bundle exec guard -w sources/foo assets/foo ./config # multiple directories

$ bundle exec guard -w /fancy/project # path outside project - watch out! (see below)
```
*NOTE: this option is only meant for ignoring subdirectories in the CURRENT
directory - by selecting which ones to actually track.*

If your watched directories are outside the current one, or if `--watchdirs` isn't working
as you expect, be sure to read: [Correctly using watchdirs](https://github.com/guard/guard/wiki/Correctly-using-the---watchdir-option)

You may find it more convenient to use the `directories` statement (described
below) in your Guardfile


#### `-G`/`--guardfile` option

Guard can use a `Guardfile` not located in the current directory:

```bash
$ bundle exec guard --guardfile ~/.your_global_guardfile
$ bundle exec guard -G ~/.your_global_guardfile # shortcut
```
*TIP: set `BUNDLER_GEMFILE` environment variable to point to your Gemfile if it isn't in the current directory or the current Gemfile doesn't include all your favorite plugins*


#### `-i`/`--no-interactions` option

Turn off completely any Guard terminal interactions with:

```bash
$ bundle exec guard start -i
$ bundle exec guard start --no-interactions
```


#### `-B`/`--no-bundler-warning` option

Skip Bundler warning when a Gemfile exists in the project directory but Guard is not run with Bundler.

```bash
$ bundle exec guard start -B
$ bundle exec guard start --no-bundler-warning
```


#### `-l`/`--latency` option

Overwrite Listen's default latency, useful when your hard-drive / system is slow.

```bash
$ bundle exec guard start -l 1.5
$ bundle exec guard start --latency 1.5
```

*NOTE: this option is OS specific: while higher values may reduce CPU usage
(and lower values may increase responsiveness) when in polling mode , it has no
effect for optimized backends (except on Mac OS). If guard is not behaving as
you want, you'll likely instead want to tweak the `--wait-for-delay` option
below or use the `--watchdirs` option.*


#### `-p`/`--force-polling` option

Force Listen polling listener usage.

```bash
$ bundle exec guard start -p
$ bundle exec guard start --force-polling
```


#### `-y`/`--wait-for-delay` option

Overwrite Listen's default wait_for_delay, useful for kate-like editors through
ssh access or when guard is annoyingly running tasks multiple times.

```bash
$ bundle exec guard start -y 1
$ bundle exec guard start --wait-for-delay 1
```

#### `-T` option

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
#### `-b`/`--bare` option

You can generate an empty `Guardfile` by running the `init` task with the bare
option:

```bash
$ bundle exec guard init --bare
$ bundle exec guard init -b # shortcut
```


### Running Guard in a VM

#### `-o`/`--listen-on` option

Use Listen's network functionality to receive file change events from the network. This is most useful for virtual machines (e.g. Vagrant) which have problems firing native filesystem events on the guest OS.

##### Suggested use:

On the host OS, you need to listen to filesystem events and forward them to your VM using the `listen` script:

```bash
$ listen -f 127.0.0.1:4000
```

Remember to configure your VM to forward the appropriate ports, e.g. in Vagrantfile:

```ruby
config.vm.network :forwarded_port, guest: 4000, host: 4000
```

Then, on your guest OS, listen to the network events but ensure you specify the *host* path

```bash
$ bundle exec guard -o '10.0.2.2:4000' -w '/projects/myproject'
```
