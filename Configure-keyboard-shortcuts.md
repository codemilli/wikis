The Guard keyboard shortcuts are in fact [signals](http://www.unix.com/man-page/All/7/signal/) that are being trapped. Signals are specified in [POSIX.1](http://www.unix.org/version3/ieee_std.html) standard and not all operating systems are full POSIX compliant (like embedded systems and windows). You can send signals to Guard with the [kill](http://www.unix.com/man-page/All/1/kill/) command on Unix like operating systems.

Guard uses the following signals:

- `SIGQUIT` => Run all
- `SIGINT` => Stop
- `SIGTSTP` => Reload

You can set the options for a terminal device interface with the [stty](http://www.unix.com/man-page/All/1/stty/) command. This allows you to list the current control characters for signals:

    $ stty -a
    cchars: discard = ^O; dsusp = ^Y; eof = ^D; eol = <undef>;
	eol2 = <undef>; erase = ^?; intr = ^C; kill = ^U; lnext = ^V;
	min = 1; quit = ^\; reprint = ^R; start = ^Q; status = ^T;
	stop = ^S; susp = ^Z; time = 0; werase = ^W;

Now you can change the control character for `SIGQUIT`:

    $ stty quit "^R"

This maps Guards' Run all to `Ctrl-R`.

If you use Guard on Windows, you should install [Cygwin](http://www.cygwin.com/) and make sure you have the [coreutils](http://cygwin.com/cgi-bin2/package-cat.cgi?file=coreutils%2Fcoreutils-8.10-1&grep=sh-utils) package installed to have the appropriate commands available in your shell.