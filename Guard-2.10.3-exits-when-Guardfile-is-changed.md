## Guard no longer reevaluates files

### The Workaround

Run Guard with this shell one-liner:

```bash
while bundle exec guard; do echo "Restarting guard..."; done
```

And now, every time you change the file, Guard exists and gets restarted by the shell script. 100% bullet proof, as opposed to how reevaluating was implemented up till now.

### Alternative workaround

You may prefer to simply binstub your guard: `bundle binstub guard` and edit the created `bin/guard` so it loops there (so you don't need a shell script).

### Problems

If guard isn't responding to changes to your Guardfile - you may need to move you `Guardfile` to another directory, and symlink it.
For more info see: [[Optimizing for large projects]]

### Background

Supporting the feature is a maintenance nightmare, because it's kind of like implementing fork() in pure Ruby in an app that heavily relies on global state. Also, since watching whole projects doesn't make sense - using the `directories` statement means the Guardfile can't be watched anyway (unless it's symlinked) and since the Guardfile isn't constantly changed and the workaround is trivial - this isn't a show-stopper by any means. 

If you strongly disagree - feel free to comment on the existing related issue(s).