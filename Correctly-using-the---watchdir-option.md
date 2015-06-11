### Intro

The `--watchdir` option (and the `directories statement in the `Guardfile`) allow watching directories other than just the current one.

Guard handles paths relative to the current directory.

So, if you're watching `foo/bar`, your watcher patterns will be matched against files like `foo/bar/baz.txt`.

This means you can watch any directories relative to the current one - without changing the patterns in your `Guardfile`.

But if you watch paths outside your project, this behavior changes (see below about absolute paths).

### Examples

```bash
$ bundle exec guard --watchdir source/files # watch a subdirectory of your project
$ bundle exec guard -w source/files # shortcut
$ bundle exec guard -w sources/foo assets/foo ./config # multiple directories

$ bundle exec guard -w . /fancy/project # path outside project - watch out! (see info below)
```

A good example use case in a Rails project may be:

```bash
# Thanks to this, we aren't tracking changes in: db, log, tmp, doc and vendor
$ bin/guard -w app config features lib public spec
```

#### Watching paths outside your project dir

E.g. if your project is in `/projects/foo` and you are watching `/foo/bar`, then your Guardfile rules would have to use *absolute* paths.

This is inconvenient, because it would force you to use absolute paths in your Guardfile. 

So the solution is to run `guard` from inside the directory containing the paths you want to watch. But since the Guardfile is in the project directory - you want to use the '-G option` to tell guard where the Guardfile is.

Example (if Guardfile is *not* where you're tracking files):

If your Guardfile is in `/projects/foo/` and the files you track are in
`/data/bar/`, you might be tempted to run:

```
$ cd /projects/foo
$ bin/guard -w /data/bar
$ echo "changes" >> /data/bar/baz
```

This won't work unless your Guardfile has `watch` statements for paths like
`../../data/bar/baz` (so regexps would have to additionally handle the
unexpected `../..` in paths).

Note: On Windows, if the paths contain different drives, you'll get full paths
containing the drive.

Since Guardfiles are more robust if tracked files are within the current
directory, you should instead consider "reversing things":

1. go to the directory where the watched files are
2. use BUNDLE_GEMFILE to point back to where your Gemfile is
3. use the -G options to point to where your Guardfile is

```
$ cd /data/bar
$ BUNDLE_GEMFILE=/projects/foo/Gemfile bundle exec guard -G /projects/foo/Guardfile
$ echo "changes" >> ./baz
```

Example rule in `Guardfile`
```ruby
watch(/^baz$/) { (...) }
```

This, way, the Guardfile becomes simple, since it will only get the relative
path 'baz' (because it's relative to current directory).
