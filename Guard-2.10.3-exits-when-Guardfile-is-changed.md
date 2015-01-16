## Problem: Guard no longer reevaluates files

### Option 1: Nice/Better/Recommended Workaround (for projects)

Just like you create binstubs, you can have a `bin/guard` file that reloads automatically.

[Just download this gist](https://gist.github.com/e2/b39b406d0f3309261558) as `bin/guard`.

### Option 2: The Quick-And-Dirty Workaround

Run Guard with this shell one-liner:

```bash
while bundle exec guard; echo "Restarting guard..."; do echo; done
```

And now, every time you change the file, Guard exits and gets restarted by the shell script. The extra `echo` in the while condition is needed as otherwise Guard exits with a non-zero status, breaking the loop.

**Note**: Ctrl-D will no longer close Guard. You can use Ctrl-C to exit Guard.

100% bullet proof, as opposed to how reevaluating was implemented up till now.

### Problems

If guard isn't responding to changes to your Guardfile - you may need to move you `Guardfile` to another directory, and symlink it.

Why so?

Since the MacOS driver pretty much can watch only recursively, you can either:

1. watch *everything*
2. or watch given directories (and their contents, recursively), but without the top directory

Since option 1 is bad for big projects, the solution is using  the `directories` statement. But if you can't then watch the top directory, you can't watch the `Guardfile`, the `Gemfile`, etc.

So the solution to this new problem (can't use `directories` *and* watch `Guardfile` at the same time), is to put `Guardfile` in a subdir (e.g. `config`), watch *that* directory, and symlink it back.

For more info see: [[Optimizing for large projects]]

### Background

Supporting the feature was a maintenance nightmare (kind of like implementing fork() in pure Ruby in an app that heavily relies on global state - and there was always something broken). 

So sorry for removing this feature - it kept the project from making any progress and we decided that with the above workarounds, it wasn't a show-stopper. But the gain was massive...