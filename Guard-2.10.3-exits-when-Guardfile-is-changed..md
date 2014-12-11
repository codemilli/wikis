#### Description

If you are watching the directory with the Guardfile (not recommended), Guard will exit so you can restart it manually.

#### History

This used to happen automatically, but the feature was dropped because it was unreasonably
expensive to maintain. On top of that, the `directories` statement makes detecting the change trickier.

For details and a workaround go here: https://github.com/guard/guard/issues/688

#### Second problem

This warning also means you are watching the *whole* project directory.

This is not recommended and can cause lots of strange issues.

#### Solution

What you should do instead (if you can) is use the `directories` statement in
the Guardfile or use the '-w` option to listen only to meaningful directories.

You will also want to move the top-level files you want to listen to a
different directory (e.g. config) watch that dir instead (see `directories`),
and symlink them back.

For details see: https://github.com/guard/guard/wiki/Optimizing-for-large-projects
