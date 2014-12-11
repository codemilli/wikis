### Quick summary

1) use the `directories` statement to watch only selected subdirectories of your project

2) move any other files you want to watch (like `Gemfile`, `Guardfile`) to one of those watched subdirectories and symlink them

(See: "Example" below)


### Short intro

Watching files for changes is especially slow and expensive on OSX and Windows (less of a problem on Linux).

The solution is to avoid watching files we don't care about - especially files that change frequently, e.g. databases and log files.

Sadly, since Apple didn't make it practical to watch files instead of directories, recursive watching and scanning cannot be currently avoided.

Since recursion cannot be disabled and people expect to watch files in their top project directories (e.g. `Gemfile`, `Guardfile`, `*.gemspec`, etc.), this implies watching *every* file in the directory.

This is ok for small projects without much going on - but people with larger projects shouldn't be paying the price.

### Workarounds

Guard does support 'ignore' options, but this only provides a major performance boost when polling (which is unacceptable for large projects anyway). This approach also needs constant tweaking and maintenance as the project grows.

The best solution is watching only subtrees of the project with frequently changed source files, like `app`, `config`, `lib`, `public`, `features`, `spec`. This automatically avoids directories like `log`, `db`, `tmp` - but it also prevents watching the above mentioned `Gemfile`, `Guardfile`, `*.gemspec`.

This can be done with the `directories` statement in your Guardfile, or with the `-w` commandline option.


### The choices

So the choices are:
* watch everything and pay the price (but avoid time spent tweaking anything)
* try to tweak the ignore rules to mitigate the problem (but waste time maintaining complex ignore rules and reorganizing the project)
* select which directories to actually watch (but you can't watch the top directory anymore)

Of course, the last one is the most reasonable.

### Example

To "have the cake and eat it", the workaround is to move the top-directory files into a watched directory and then symlink them, e.g.

```bash
$ mkdir config
$ git mv Gemfile config
$ ln -s config/Gemfile .
$ git add Gemfile
```

and do the same for other watched files, like `Guardfile`, `*.gemspec`, `Gemfile`, etc.

Then, add `config` to the watched directories (if it isn't watched already) in your Guardfile:

```
directories %w(app config lib public features test spec)
```

### Windows

Depends on the Windows version, though there are tools for creating symlinks like `junction` and `mklink.exe`.
