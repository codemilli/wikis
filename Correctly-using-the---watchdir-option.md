#### Summary: Run guard where the tracked files are (by using the `-G` option), unless you want to adapt your Guardfile to handling "strange" paths.

Guard can watch any number of specified sub-directories (instead of only the current directory):

```bash
$ bundle exec guard --watchdir source/files # watch a subdirectory of your project
$ bundle exec guard -w source/files # shortcut
$ bundle exec guard -w sources/foo assets/foo ./config # multiple directories

$ bundle exec guard -w . /fancy/project # path outside project - watch out! (see info below)
```
*NOTE: this option is only meant for ignoring sub-directories relative to the CURRENT
directory - by selecting which ones to actually track.*

A good example use case in a Rails project may be:

```bash
# Thanks to this, we aren't tracking changes in: db, log, tmp, doc and vendor
$ bin/guard -w app config features lib public spec
```

*NOTE: if you aren't tracking a sub-directory of the CURRENT directory, your
Guardfile may have to be adapted to respond to changes*

Example (if Guardfile is *not* where you're tracking files):

If your Guardfile is in `/projects/foo/` and the files you track are in
`/data/bar/`, you might be tempted to run:

```
$ cd /projects/foo
$ bin/guard -w /data/bar
$ echo "changes" >> /data/bar/baz
```

Surprisingly, your Guardfile would have to handle paths like
`../../data/bar/baz` (so regexps would have to additionally handle the
unexpected `../..` in paths).

Note: On Windows, if the paths contain different drives, you'll get full paths
containing the drive.

Since Guardfiles are more robust if tracked files are within the current
directory, you should instead consider:

```
$ cd /data/bar
$ BUNDLER_GEMFILE=/projects/foo/Gemfile bundle exec guard -G /projects/foo/Guardfile
$ echo "changes" >> ./baz
```

This, way, the Guardfile becomes simple, since it will only get the relative
path 'baz' (because it's relative to current directory).

