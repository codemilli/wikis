Here's a list of know "alternatives" to Guard.

(The order should be: how generally feature-complete the tool is compared to Guard)

Feel free to add/update entries and notes/caveats/differences.

### Close in functionality to Guard
- [watchdog](https://github.com/gorakhargosh/watchdog) - in Python
- [nodemon](https://github.com/remy/nodemon) - has a '-x' option

### File-config based with built-in execution:
- [gulp](https://github.com/gulpjs/gulp/blob/master/docs/getting-started.md)
- [gamin](https://people.gnome.org/~veillard/gamin/config.html)
- [belvedere](http://lifehacker.com/341950/belvedere-automates-your-self-cleaning-pc) - Windows only, seems ancient
- [watch-4-folder](http://leelusoft.blogspot.in/2011/10/watch-4-folder-23.html) - Windows only, seems ancient

### Library + CLI:
- [fsmonitor](https://www.npmjs.com/package/fsmonitor)

### Non-trivial CLI tools with built-in execution:
- [entrproject](http://entrproject.org/)
- [fswatch](https://github.com/emcrisostomo/fswatch)

#### Simple CLI tools with built-in execution:
- [when-changed](https://github.com/joh/when-changed) - written in Python
- [incron](http://inotify.aiken.cz/?section=incron&page=about&lang=en) - Linux only, root only
- [inoticoming](http://manpages.ubuntu.com/manpages/natty/en/man1/inoticoming.1.html) - watches dirs
- [watchfile](http://swarminglogic.com/jotting/2014_02_watchfile)
- [when_changed](https://github.com/benblamey/when_changed) - Windows only
- [java-file-change-watcher](https://github.com/yankee42/java-file-change-watcher)

#### Simple watch-only scripts, no execution built in:
- [inotifywait](https://github.com/rvoicilas/inotify-tools/wiki)
- [wait_on](https://trac.macports.org/browser/trunk/dports/sysutils/wait_on/Portfile) - for BSD
- [sleep_until_modified.py](https://bitbucket.org/denilsonsa/small_scripts/src/542edd54d290d476603e939027ca654b25487d85/sleep_until_modified.py?at=default)
- [sleep_until_modified.sh](https://bitbucket.org/denilsonsa/small_scripts/src/542edd54d290d476603e939027ca654b25487d85/sleep_until_modified.sh?at=default)
- [kqwait](https://github.com/sschober/kqwait) - for OSX

#### Other
- [launchd](https://en.wikipedia.org/wiki/Launchd) - although it only watches for path changes, not content changes
- [pyinotify](https://github.com/seb-m/pyinotify)
- [unison](https://webdav.seas.upenn.edu/viewvc/unison/trunk/src/fsmonitor.py?view=markup&pathrev=471)
- [jnotify](http://jnotify.sourceforge.net)
- [file.monitor](https://github.com/pke/file.monitor)
- [pyfilesystem](https://github.com/PyFilesystem/pyfilesystem)


#### Other sources of alternatives
- [StackOverflow question 1](http://superuser.com/questions/181517/how-to-execute-a-command-whenever-a-file-changes/778876#778876)
- [StackOverflow question 2](http://stackoverflow.com/questions/1515730/is-there-a-command-like-watch-or-inotifywait-on-the-mac)
