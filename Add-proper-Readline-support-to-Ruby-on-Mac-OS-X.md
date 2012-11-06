If you are on Mac OS X and have problems with either Guard not reacting to file changes or Pry behaving strange, then you probably suffer under a Ruby build that uses `libedit` instead of `readline`.

If you are not using Mac OS X or are using JRuby, then you're fine.

## Using a pure Ruby readline implementation

The easiest way to get a working readline implementation is to install [rb-readline](https://github.com/luislavena/rb-readline), pure Ruby readline implementation. You can install it by simply adding

```Ruby
group :development do
  gem 'rb-readline'
end
```

to your `Gemfile` and install it with `bundle exec`.

## Build Ruby with GNU readline

## Using RVM

You can use [RVM](https://rvm.io/) to build your Ruby with GNU readline support. First install the readline package with RVM:

```Bash
$ rvm pkg install readline --verify-downloads 1
```

Then configure RVM to use the readline package by adding

```Bash
ruby_configure_flags=--enable-shared --disable-install-doc --with-readline-dir="$rvm_path/usr"
```

to `~/.rvm/user/db`. Finally you need to reinstall your Ruby of choice:

```Bash
$ rvm reinstall 1.9.2
```

## Using RVM and Homebrew

You can also install the latest Readline with [Homebrew](http://mxcl.github.com/homebrew/). First install Readline:

```Bash
$ brew install readline
```

Then configure RVM to use the Homebrew readline by adding

```Bash
ruby_configure_flags=--enable-shared --disable-install-doc --with-readline-dir=$(brew --prefix readline)
```

to `~/.rvm/user/db`. Finally you need to reinstall your Ruby of choice:

```Bash
$ rvm reinstall 1.9.2
```