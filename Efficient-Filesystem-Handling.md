Various operating systems are willing to notify you of changes to files, but the API to register/receive updates varies (see [rb-fsevent](https://github.com/thibaudgg/rb-fsevent) for OS X, [rb-inotify](https://github.com/nex3/rb-inotify) for Linux, and [rb-fchange](https://github.com/stereobooster/rb-fchange) for Windows). Guard uses the Listen gem to install all these adapters, and will select the one most appropriate for your platform. If Guard is forced to fall back to polling it will give you a warning about it doing so.

If you're using Windows and at least Ruby 1.9.2, then please add [Windows Directory Monitor](https://github.com/Maher4Ever/wdm) gem to your Gemfile to support it.

```Ruby
group :development do
  gem 'wdm', :platforms => [:mswin, :mingw], :require => false
end
```