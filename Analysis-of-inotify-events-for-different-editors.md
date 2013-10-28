This page collects information about the fired [inotify](http://en.wikipedia.org/wiki/Inotify) events that different Linux editors fires on file modification. The events are collected using  [inotifywatch](http://linux.die.net/man/1/inotifywatch).

Steps to add an event analysis of your editor: 

1. Open the file
2. Launch inotifywatch
3. Change the file content
4. Save the file
5. Quit inotifywatch

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

    total  attrib  delete_self  filename
    3      1       1            coffee/script.coffee

## Vim

    total  attrib  move_self  delete_self  filename
    4      1       1          1            coffee/script.coffee

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
