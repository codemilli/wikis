This page collects information about the fired [inotify](http://en.wikipedia.org/wiki/Inotify) events that different Linux editors fires on file modification. The events are collected using  [inotifywait](http://linux.die.net/man/1/inotifywait).

Steps to add an event analysis of your editor:

1. Open the file
2. Launch `inotifywait -m .` in the **directory** containing the file
3. Change the file content
4. Save the file
5. Quit inotifywait

**IMPORTANT NOTE**: Remember to watch the **directory** containing the file, not the file itself!

# Results

## RubyMine (v3.2.4 && v4.0EAP, Lucid 64)

Manual and auto-save events are currently indistinguishable
To disable RubyMine's auto-save/synchronization feature: `File > Settings > General`

    total  attrib  delete_self  filename
    3      1       1            coffee/script.coffee

## Sublime Text

    total  modify  close_write  open  filename
    5      3       1            1     coffee/script.coffee

## Sublime Text 3 on Linux

Given a file coffee/script.coffee and watching the coffee dir:

```
% inotifywait -m coffee
Setting up watches.
Watches established.
./ CREATE .sublc0f.tmp
./ OPEN .sublc0f.tmp
./ ATTRIB .sublc0f.tmp
./ MODIFY .sublc0f.tmp
./ CLOSE_WRITE,CLOSE .sublc0f.tmp
./ ATTRIB .sublc0f.tmp
./ MOVED_FROM .sublc0f.tmp
./ MOVED_TO script.coffee
```

Note how there's only 1 event actually on the directory: MOVED_TO.

(This is because Sublime calls rename() without deleting the file, which makes Guard think it's a new file, which calls the run_on_additions plugin method - a method many guard plugins don't implement).

## Kate

Details:

1. Kate creates a backup file, e.g. `foo.rb` -> `foo.rb~` (suffix is configurable)

2. Kate uses QTemporaryFile with a template "XXXXXX.new", which means e.g. `foo.rb` -> `foo.rbo53241.new` [(see: qtemporaryfile.cpp)](https://qt.gitorious.org/qt/qt/source/cfa01206e38d120c0ddb17aec7358aadff30b6f5:src/corelib/io/qtemporaryfile.cpp)

3. Kate uses "overwrite" technique to allow saving file in read-only directories: `foo.rbo53241.new` -> `foo.rb` (no delete happens)


E.g.:



    [:delete]: users_controller_spec.rb~
    [:moved_to, :move]: users_controller_spec.rb~
    [:attrib]: users_controller_spec.rb~
    [:create]: users_controller_spec.rbo22583.new
    [:attrib]: users_controller_spec.rbo22583.new
    [:close_write, :close]: users_controller_spec.rbo22583.new
    [:close_write, :close]: users_controller_spec.rbo22583.new
    [:moved_from, :move]: users_controller_spec.rbo22583.new
    [:moved_to, :move]: users_controller_spec.rb


## Vim

    total  attrib  move_self  delete_self  filename
    4      1       1          1            coffee/script.coffee

Details: The events Vim generates during saving actually depends on options, e.g. backup/backupdir/patchmode/backupcopy/writebackup/backupskip


## Gedit

    total  access  attrib  close_write  close_nowrite  open  delete_self  filename
    8      1       1       1            1              2     1            coffee/script.coffee

## Nano

    total  modify  close_write  open  filename
    5      3       1            1     coffee/script.coffee

## Joe

    total  access  modify  attrib  close_write  close_nowrite  open  filename
    10     1       4       1       1            1              2     coffee/script.coffee

## JEdit

    total  move_self  filename
    1      1          coffee/script.coffee

## SciTE

    total  modify  close_write  open  filename
    5      3       1            1     coffee/script.coffee

## Bluefish

    total  attrib  close_write  open  filename
    4      2       1            1     coffee/script.coffee

## echo 'foo' > coffee/test.txt

    total  modify  close_write  open  filename
    4      2       1            1     coffee/test.txt

## Redcar 0.12
    total  modify  close_write  open  filename
    4      2       1            1     coffee/script.coffee

## emacs 24

    total  access  modify  close_write  close_nowrite  open  filename
    9      1       2       1            2              3     my/fine/file

## sed

    Sed uses the "overwrite with move" trick.

    from running: `sed -e 's/a/b/' -i index.html`

    ./ OPEN index.html
    ./ CREATE sedBF20nx
    ./ OPEN sedBF20nx
    ./ MODIFY sedBF20nx
    ./ MODIFY sedBF20nx
    ./ MODIFY sedBF20nx
    ./ MODIFY sedBF20nx
    ./ ATTRIB sedBF20nx
    ./ ATTRIB sedBF20nx
    ./ CLOSE_NOWRITE,CLOSE index.html
    ./ CLOSE_WRITE,CLOSE sedBF20nx
    ./ MOVED_FROM sedBF20nx
    ./ MOVED_TO index.html
