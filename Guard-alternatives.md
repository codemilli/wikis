Here's a list of know "alternatives" to Guard.

(The order should be: how generally feature-complete the tool is compared to Guard)

Feel free to add/update entries and notes/caveats/differences.

### File-config based with built-in execution:
- [nodemon](https://github.com/remy/nodemon) - has a '-x' option
- [gulp](https://github.com/gulpjs/gulp/blob/master/docs/getting-started.md)
- [belvedere](http://lifehacker.com/341950/belvedere-automates-your-self-cleaning-pc) - Windows only, seems ancient
- [watch-4-folder](http://leelusoft.blogspot.in/2011/10/watch-4-folder-23.html) - Windows only, seems ancient

### Library + CLI:
- [fsmonitor](https://www.npmjs.com/package/fsmonitor)

### Non-trivial CLI tools with built-in execution:
- [entrproject](http://entrproject.org/)
- [fswatch](https://github.com/emcrisostomo/fswatch)

#### Simple CLI tools with built-in execution:
- [incron](http://inotify.aiken.cz/?section=incron&page=about&lang=en)
- [when-changed](https://github.com/joh/when-changed) - written in Python
- [watchfile](http://swarminglogic.com/jotting/2014_02_watchfile)
- [when_changed](https://github.com/benblamey/when_changed) - Windows only
- [java-file-change-watcher](https://github.com/yankee42/java-file-change-watcher)

#### Simple watch-only scripts, no execution built in:
- [inotifywait](https://github.com/rvoicilas/inotify-tools/wiki)
- [wait_on](https://trac.macports.org/browser/trunk/dports/sysutils/wait_on/Portfile) - for BSD
- [sleep_until_modified.py](https://bitbucket.org/denilsonsa/small_scripts/src/542edd54d290d476603e939027ca654b25487d85/sleep_until_modified.py?at=default)
- [sleep_until_modified.sh](https://bitbucket.org/denilsonsa/small_scripts/src/542edd54d290d476603e939027ca654b25487d85/sleep_until_modified.sh?at=default)

#### Other
- [launchd](https://en.wikipedia.org/wiki/Launchd) - although it only watches for path changes, not content changes

#### Other sources of alternatives
- [StackOverflow question 1](http://superuser.com/questions/181517/how-to-execute-a-command-whenever-a-file-changes/778876#778876)
- [StackOverflow question 2](http://stackoverflow.com/questions/1515730/is-there-a-command-like-watch-or-inotifywait-on-the-mac)