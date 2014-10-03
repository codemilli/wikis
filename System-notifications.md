You can configure Guard to notify plugin results throgh one or more channels described below. If you
do not specify a specific notification channel with the
[notification](https://github.com/guard/guard#notification) DSL method, then Guard auto-detects all
available channels and makes use of them.

## Ruby GNTP

* Runs on Mac OS X, Linux and Windows
* Supports [Growl](http://growl.info/) version >= 1.3, [Growl for Linux](http://mattn.github.com/growl-for-linux/),
  [Growl for Windows](http://www.growlforwindows.com/gfw/default.aspx) and
  [Snarl](https://sites.google.com/site/snarlapp/home)

The [ruby_gntp](https://rubygems.org/gems/ruby_gntp) gem sends system notifications over the network with the
[Growl Notification Transport Protocol](http://www.growlforwindows.com/gfw/help/gntp.aspx) and supports local and
remote notifications. To have the images be displayed, you have to use `127.0.0.1` instead of `localhost` in your GNTP
configuration.

Guard supports multiple notification channels for customizing each notification type. For Growl on Mac OS X you need
to have at least version 1.3 installed.

To use `ruby_gntp` you have to add it to your `Gemfile` and run bundler:

```ruby
group :development do
  gem 'ruby_gntp'
end
```

## Growl

* Runs on Mac OS X
* Supports all [Growl](http://growl.info/) versions

The [growl](https://rubygems.org/gems/growl) gem is compatible with all versions of Growl and uses a command line tool
[growlnotify](http://growl.info/extras.php#growlnotify) that must be separately downloaded and installed. The version of
the command line tool must match your Growl version. The `growl` gem does **not** support multiple notification
channels.

You have to download the installer for `growlnotify` from the [Growl download section](http://growl.info/downloads).

To use `growl` you have to add it to your `Gemfile` and run bundler:

```ruby
group :development do
  gem 'growl'
end
```

## Libnotify

* Runs on Linux, FreeBSD, OpenBSD and Solaris
* Supports [Libnotify](http://developer.gnome.org/libnotify/)

The [libnotify](https://rubygems.org/gems/libnotify) gem supports the Gnome libnotify notification daemon, but it can be
used on other window managers as well. You have to install the `libnotify-bin` package with your favorite package
manager.

To use `libnotify` you have to add it to your `Gemfile` and run bundler:

```ruby
group :development do
  gem 'libnotify'
end
```

If you are unable to build the `libnotify` gem on your system, Guard
also has a built in notifier - `notifysend` - that shells out to the
`notify-send` utility that comes with `libnotify-bin`.

## Notifu

* Runs on Windows
* Supports [Notifu](http://www.paralint.com/projects/notifu/)

The [rb-notifu](https://rubygems.org/gems/rb-notifu) gem supports Windows system tray notifications.

To use `rb-notifu` you have to add it to your `Gemfile` and run bundler:

```ruby
group :development do
  gem 'rb-notifu'
end
```

## Terminal Notifier

* Runs on Mac OS X 10.8 only

The [terminal-notifier-guard](https://github.com/Springest/terminal-notifier-guard) sends notifications to the OS X
Notification Center.

To use `terminal-notifier-guard` you have to add it to your `Gemfile` and run bundler:

```ruby
group :development do
  gem 'terminal-notifier-guard'
end
```

## Terminal Title

* Runs in every terminal supporting XTerm escape sequences to set the window title.

## Emacs

* Runs on any platform with Emacs + emacsclient (http://www.emacswiki.org/emacs/EmacsClient)

## TMux

* To use TMux notifications, you have to start Guard within a [TMux](http://tmux.sourceforge.net/) session.

The TMux notifier will color the background of the left part of the
status bar indicating the status of the notifications. Optionally you
can set `:display_message => true` to display the Guard notification as
'display-message' notification.

The way these messages are formatted is configurable.

```ruby
# Guardfile
notification :tmux,
  display_message: true,
  timeout: 5, # in seconds
  default_message_format: '%s >> %s',
  # the first %s will show the title, the second the message
  # Alternately you can also configure *success_message_format*,
  # *pending_message_format*, *failed_message_format*
  line_separator: ' > ', # since we are single line we need a separator
  color_location: 'status-left-bg' # to customize which tmux element will change color
```
The color location option can also take an array:

```
color_location: %w[status-left-bg pane-active-border-fg pane-border-fg]
```

The result will be for RSpec using example above

    RSpec >> 15 test, 0 failures > in 0.002 sec

You can use nice powerline chars here if you have that configured.

You can get the message history by using `Ctrl+b ~` (where `Ctrl+b` is your key to activate TMux).

## File

* You can also have Guard write notifications to a file. Each notification will
  overwrite the file. This allows other commands to be run based on the status
  of other guard commands.

Example:

```ruby
# Guardfile
notification :file, path: '.guard_result'

guard :shell do
  watch '.guard_result' do
    if File.read('.guard_result').lines.first.strip == 'failed'
      # ...
    end
  end
end
```

Configuration:

```ruby
# Guardfile
notification :file,
  path: '.guard_result', # Required, no default
  format: "result: %s\ntitle: %s\nmessage: %s\n" # Default: "%s\n%s\n%s\n"
```