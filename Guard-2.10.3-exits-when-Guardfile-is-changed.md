## Guard no longer reevaluates files

### The Workaround

Run Guard with this shell one-liner:

```bash
while bundle exec guard; do echo "Restarting guard..."; done
```

And now, every time you change the file, Guard exists and gets restarted by the shell script. 100% bullet proof, as opposed to how reevaluating was implemented up till now.

If guard doesn't respond - you may need to move you `Guardfile` to another directory, and symlink it.

For more info see: [[Optimizing for large projects]]