How about using the [notify](https://github.com/jugyo/notify) gem for handle notifications?

I can't install the `growl_notify` gem on Linux because it depends on the [rb-appscript](http://appscript.sourceforge.net/rb-appscript/index.html) gem, which doesn't compile outside Mac. This is a problem because we put our `Gemfile.lock` file under version control.