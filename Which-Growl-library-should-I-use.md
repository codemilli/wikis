***
Try `ruby_gntp` first, use `growl` when you have some problems with it.
***

If you like to have [Growl](http://growl.info/) notifications on Mac OS X, you can choose between the following:

* [ruby_gntp](https://github.com/snaka/ruby_gntp)
* [growl](https://github.com/visionmedia/growl)
* [growl_notify](https://github.com/scottdavis/growl_notify) 

The difference is how these gems interacts with Growl: **growl_notify** uses applescript bindings through [rb-appscript](http://appscript.sourceforge.net/rb-appscript/index.html), **ruby_gntp** sends network packages via the Growl Notification Transport Protocol and  **growl** executes the `growlnotify` command.

The benefit of both growl_notify and ruby_gntp is that you don't have to [download](http://growl.info/extras.php) and install the `growlnotify` command manually, so this is generally the recommended way of getting growl support.

The downside of growl_notify is that there are some known issues:

* It doesn't work on Rubinius due to a bug in rb-appscript.
* It doesn't work on MacRuby.
* It _may_ give you an [exception](https://gist.github.com/1151368) when using with [Spork](https://github.com/timcharper/spork), but others have reported that it works well.

If growl (and/or growlnotify) are working outside of Guard, but are not working when you use rspec via spork, make absolutely sure that the environment variable SPEC_OPTS is not set.  If it is, it will take precedence over the arguments spork passes to rspec invaliding the custom formatter requested (which is what is responsible for making the notifications)

Please feel free to add your experience.

