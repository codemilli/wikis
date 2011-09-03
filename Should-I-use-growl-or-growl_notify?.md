If you like to have [Growl](http://growl.info/) notifications on Mac OS X, you can choose between [growl_notify](https://github.com/scottdavis/growl_notify) and the older [growl](https://github.com/visionmedia/growl) gems.

The difference is how these gems interacts with Growl: **growl_notify** uses applescript bindings through [rp-appscript](http://appscript.sourceforge.net/rb-appscript/index.html), whereas **growl** executes the `growlnotify` command.

The benefit of growl_notify is that you don't have to [download](http://growl.info/extras.php) and install the `growlnotify` command manually.