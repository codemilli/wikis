Here are problems Guard helps avoid (compared to other scripts or tools like inotify-wait):

1. easier to run, manage and extend/maintain:
- just generate and edit a Guardfile (once) and run `guard`
- nice, readable [DSL](https://github.com/guard/guard/wiki/Guardfile-DSL---Configuring-Guard) for setting complex rules
- in Ruby
- simple example templates are generated for you
- well documented, lots of simple examples
- fantastic community support (just file an issue and see...)
- built in support for logging and notification (Growl, etc.)

1. more efficient:
- allows efficiently talking with servers (connect once on startup, then make request every change)
- scans large directories only once on startup
- no "sleep" code needed - changes can happen either immediately, or they can be "accumulated" and "compressed" (to avoid running the command too frequently)


1. more robust and "correct":

- properly handled cases when files are changed while the command is running
- no inotifywait/inotifywatch errors to deal with
- watches the files directory, so it supports file adding, renames (which is what editors do - they rarely just "modify" a file in place)
- interactive console to rerun, simulate and debug events
- Guard itself reloads when you change it's configuration
- single instance of Guard can handle many directories (instead of running many unmanageable "instances" of inotify_wait scripts running)
- more than 7 million gem downloads and almost no open issues
- handles moving whole files and directories

1. more portabile:
- supports multiple platforms (Linux, OSX, BSD, Windows)
- supports multiple backends (inotify, kqueue, polling)
- polling for network drives and VM shared dirs (which don't support inotify)

