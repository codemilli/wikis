Various operating systems are willing to notify you of changes to files, but the API to register/receive updates varies (see [rb-fsevent](https://github.com/thibaudgg/rb-fsevent) for OS X, [rb-inotify](https://github.com/nex3/rb-inotify) for Linux, and [rb-fchange](https://github.com/stereobooster/rb-fchange) for Windows). Guard uses the Listen gem to install all these adapters, and will select the one most appropriate for your platform. If Guard is forced to fall back to polling it will give you a warning about it doing so.

A challenge arises when trying to make these dependencies work with [Bundler](http://gembundler.com/). If you simply put one of these dependencies into your `Gemfile`, even if it is conditional on a platform match, the platform-specific gem will end up in the `Gemfile.lock`, and developers will thrash the file back and forth.

There is a good solution. All three gems will successfully, quietly install on all three operating systems, and `guard/listen` will only pull in the one you need. This is a more proper `Gemfile`, and this is what Listen will do for you:

```Ruby
group :development do
  gem 'rb-inotify', :require => false
  gem 'rb-fsevent', :require => false
  gem 'rb-fchange', :require => false
end
```

If you're using Windows and at least Ruby 1.9.2, then [Windows Directory Monitor](https://github.com/Maher4Ever/wdm) is more efficient than using `rb-fchange`.

```Ruby
group :development do
  gem 'wdm', :platforms => [:mswin, :mingw], :require => false
end
```