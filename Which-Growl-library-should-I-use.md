***
Try `ruby_gntp` first, use `growl` when you have some problems with it.
***

If you like to have [Growl](http://growl.info/) notifications on Mac OS X, you can choose between the following:

* [ruby_gntp](https://github.com/snaka/ruby_gntp)
* [growl](https://github.com/visionmedia/growl)

The difference is how these gems interacts with Growl: **ruby_gntp** sends network packages via the Growl Notification Transport Protocol and  **growl** executes the `growlnotify` command.

The benefit of ruby_gntp is that you don't have to [download](http://growl.info/extras.php) and install the `growlnotify` command manually, so this is generally the recommended way of getting growl support.

If growl (and/or growlnotify) are working outside of Guard, but are not working when you use rspec via spork, make absolutely sure that the environment variable SPEC_OPTS is not set.  If it is, it will take precedence over the arguments spork passes to rspec invaliding the custom formatter requested (which is what is responsible for making the notifications)

Please feel free to add your experience.

