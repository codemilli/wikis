***
Try `ruby_gntp` first, use `growl` when you have some problems with it.
***

If you like to have [Growl](http://growl.info/) notifications on Mac OS X, you can choose between the following:

* [ruby_gntp](https://github.com/snaka/ruby_gntp)
* [growl](https://github.com/visionmedia/growl)
* [growl_notify](https://github.com/scottdavis/growl_notify) 

The difference is how these gems interacts with Growl: **growl_notify** uses applescript bindings through [rb-appscript](http://appscript.sourceforge.net/rb-appscript/index.html), **ruby_gntp** sends network packages via the Growl Notification Transport Protocol and  **growl** executes the `growlnotify` command.

The benefit of both growl_notify and ruby_gntp is that you don't have to [download](http://growl.info/extras.php) and install the `growlnotify` command manually, so this is generally the recommended way of getting growl support. If you have [Homebrew](http://mxcl.github.com/homebrew/) installed, you'd simply install growlnotify with `brew install growlnotify`.

The downside of growl_notify is that there are some known issues:

* It doesn't work on Rubinius due to a bug in rb-appscript.
* It doesn't work on MacRuby.
* It _may_ give you an [exception](https://gist.github.com/1151368) when using with [Spork](https://github.com/timcharper/spork), but others have reported that it works well.

Please feel free to add your experience.