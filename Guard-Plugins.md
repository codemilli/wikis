(Order: by area: popularity among beginners or ideally by star count)

NOTE: some plugin authors work on their own forks instead of the forks in the Guard organization. Please update the links below if they point to the wrong/outdated fork.

## Rails related

| Plugin | When to use |
| ------ | ------------|
| guard-jammit |  Compressing assets (JS, CSS)
| guard-zeus |  Zeus speeds up startup time for Rails commands (development, server, testing)
| guard-annotate |  Inserts "cheatsheets" about your database schema into your source files
| guard-passenger |  Manages the Passenger server (restarts when necessary)
| guard-sprockets |  Recompiles assets using Sprockets
| guard-migrate |  Migrates the database whenever you add/change migrations
| guard-brakeman |  Scans your Rails application for known security holes (CVE's)
| guard-rails_best_practices | check if code matches Rails Best Practices

## General Web Development & Design

| Plugin | When to use |
| ------ | ------------|
| guard-jekyll-plus |  Extensive plugin for working with Jekyll projects
| guard-middleman |  Rebuilds Middleman static websites
| guard-coffeescript |  Compiles CoffeeScript files
| guard-compass |  Rebuilds your CSS files in Compass Sass projects
| guard-sass |  Recompiles Sass files to CSS
| guard-steering |  Speed up Handlebar.js templates by precompiling them
| guard-webrick |  Restarts WEBrick server when needed
| guard-pusher |  Send messages to multiple iPad/iPhone browsers (like "reload page")
| guard-shopify |  automatically upload and update Shopify templates when they change
| guard-slim |  regenerate slim templates
| guard-premailer |  inline CSS in email templates
| guard-uglify |  compress JavaScript files using uglifier gem

## Testing

| Plugin | When to use |
| ------ | ------------|
| guard-cucumber |  Reruns changed/affected Cucumber Features
| guard-teaspoon |  Web testing with PhantomJS or Selenium WebDriver
| guard-motion |  reruns specs for RubyMotion (iOS, Android, OSX Ruby apps)
| guard-phpunit |  Guard::PHPUnit automatically runs your tests
| guard-frank |  rerun Frank-Cucumber (iOS) features
| guard-calabash-ios |  return Calabash iOS Cucumber features
| guard-jasmine-headless-webkit |  rerun Jasmine tests in a headless WebKit instance
| guard-jasmine-node |  reruns Jasmine Node.js tests
| guard-jenkins |  sets a Jenkins status image depending whether there's a failure or not
| guard-prove |  reruns Perl tests

### Code Quality
| Plugin | When to use |
| ------ | ------------|
| guard-cane |  fails the build if your source files fail the quality level
| guard-rubocop |  Check your source files to style violations and potential problems
| guard-jshint-node |  detect errors and potential problems in JavaScript files

### Documentation
| Plugin | When to use |
| ------ | ------------|
| guard-hologram |  generates beautiful style guides for CSS
| guard-docbook-status |  update docbook document overviews (structure stats)
| guard-readme-on-github |  preview GitHub pages locally before pushing them to GH
| guard-rocco |  regenerates Rocco docs
| guard-gimli |  convert markup files (markdown, rdoc) into PDF files
| guard-git-scribe |  rebuild git-scribe ebooks
| guard-markdown |  convert Markdown files to HTML

### DevOps

| Plugin | When to use |
| ------ | ------------|
| guard-s3 |  Synchronize folders with Amazon S3 buckets
| guard-puppet |  Helps build Puppet catalogs for deploying and managing sites and servers
| guard-chef |  watches and reloads Chef recipes automatically
| guard-flopbox |  synchronize directories via SFTP

### Utility

| Plugin | When to use |
| ------ | ------------|
| guard-ctags-bundler |  regenerates CTags files so editors can find method definitions
| guard-shell |  Runs shell commands when changes happen - also supports notifications and long -running programs
| guard-go |  Run and restart go programs and servers when changed
| guard-rake |  reruns a rake task when files change
| guard-redis |  restarts Redis server when needed
| guard-rsync |  automatically sync directories with RSync whenever they change
| guard-resque |  restarts Resque workers
| guard-delayed |  automatically restarts delayed_job workers
| guard-sprite-factory | Web Development | regenerate CSS sprites from a series of images
| guard-post |  automatically load text files into database records (Mongoid, ActiveRecord, etc.)
| guard-lilypond | Engraving music scores
| guard-zen |  Runs Ruby Koans

NOTE: if any above plugins are broken or outdated, try the following:
1. find the gem on rubygems.org, then go to the homepage
2. file an issue there and wait up to a few days for the author to respond
3. if the plugin author isn't responding CC a Guard maintainer in the issue (e.g. me: @e2)

### Outdated/Obsolete plugins

| Outdated Plugin | Why outdated/obsolete |
| ------ | -------- |
| guard-spring | guard-rspec supports running RSpec with Spring and a lot more
| guard-rails-assets | not sure if it works with Rails 4
| guard-jekyll | superseeded by guard-jekyll-plus
| guard-rspectacle | Embedded RSpec runner - probably better to use Guard::Rspec or Guard::Zeus
| guard-coffeedripper | probably outdated
| guard-focus | probably can be replaces with Guard::RSpec with custom config
| guard-jessie | likely superseeded by guard-jasmine
| guard-stitch | alternative to guard-sprockets, but may be outdated
| guard-db | probably replaced with guard-migrate
| Rails-Autotester | probably replaced with Guard::Minitest
| guard-sprockets2 | probably outdated
| guard-hydra | probably replaced with Guard::RSpec using parallel specs (check Guard::RSpec Readme)
| guard-ego | Guard can now reload itself
| guard-jslint-on-rails | probably outdated
| guard-mozrepl | probably superseeded by Guard::LiveReload
| guard-jstd | probably superseeded by other JavaScript testing Guard plugins
| guard-phantomjs | probably superseeded by other JavaScript testing Guard plugins
| guard-krl | updates cloud-based Kinetic Rules Engine rule files (company dissolved)
| guard-soca | likely outdated
| guard-stendhal | likely outdated
| guard-autorefresh | superseeded by Guard::LiveReload
