If you like to have [Growl](http://growl.info/) notifications on Mac OS X, you can choose between [growl_notify](https://github.com/scottdavis/growl_notify) and the older [growl](https://github.com/visionmedia/growl) gems.

The difference is how these gems interacts with Growl: **growl_notify** uses applescript bindings through [rp-appscript](http://appscript.sourceforge.net/rb-appscript/index.html), whereas **growl** executes the `growlnotify` command.

The benefit of growl_notify is that you don't have to [download](http://growl.info/extras.php) and install the `growlnotify` command manually, so this is generally the recommended way of getting growl support.

The downside of growl_notify is, that there are some known issues:
* It doesn't work with Rubinius due to a bug in rb-appscript.
* It _may_ give you an exception when using with [Spork](https://github.com/timcharper/spork), but others have reported that it works well.