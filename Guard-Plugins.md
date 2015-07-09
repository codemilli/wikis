(Order: by area: popularity among beginners or ideally by star count)

NOTE: some plugin authors work on their own forks instead of the forks in the Guard organization. Please update the links below if they point to the wrong/outdated fork.

| Plugin | Area | When to use |
| ------ | ---- | ------------|
| guard-jammit | Rails | Compressing assets (JS, CSS)
| guard-zeus | Rails | Zeus speeds up startup time for Rails commands (development, server, testing)
| guard-annotate | Rails | Inserts "cheatsheets" about your database schema into your source files
| guard-passenger | Rails | Manages the Passenger server (restarts when necessary)
| guard-sprockets | Rails | Recompiles assets using Sprockets
| guard-migrate | Rails | Migrates the database whenever you add/change migrations
| guard-jekyll-plus | Web Development | Extensive plugin for working with Jekyll projects
| guard-middleman | Web Development | Rebuilds Middleman static websites
| guard-coffeescript | Web Development | Compiles CoffeeScript files
| guard-compass | Web Development | Rebuilds your CSS files in Compass Sass projects
| guard-sass | Web Development | Recompiles Sass files to CSS
| guard-steering | Web Development | Speed up Handlebar.js templates by precompiling them
| guard-cucumber | Testing | Reruns changed/affected Cucumber Features
| guard-cane | Code Quality | fails the build if your source files fail the quality level
| guard-ctags-bundler | IDE | regenerates CTags files so editors can find method definitions
| guard-rubocop | Code Quality | Check your source files to style violations and potential problems
| guard-brakeman | Rails | Scans your Rails application for known security holes (CVE's)
| guard-shell | Utility | Runs shell commands when changes happen - also supports notifications and long -running programs
| guard-hologram | Documentation | generates beautiful style guides for CSS
| guard-teaspoon | Testing | Web testing with PhantomJS or Selenium WebDriver
| guard-lilypond | Music | Engraving music scores
| guard-s3 | DevOps | Synchronize folders with Amazon S3 buckets
| guard-puppet | DevOps | Helps build Puppet catalogs for deploying and managing sites and servers
| guard-webrick | Web Development | Restarts WEBrick server when needed
| guard-go | Utility | Run and restart go programs and servers when changed
| guard-motion | Testing | reruns specs for RubyMotion (iOS, Android, OSX Ruby apps)
| guard-phpunit | Testing | Guard::PHPUnit automatically runs your tests
| guard-rake | Utility | reruns a rake task when files change
| guard-docbook-status | Documentation | update docbook document overviews (structure stats)
| guard-pusher | Web Development | Send messages to multiple iPad/iPhone browsers (like "reload page")
| guard-frank | Testing | rerun Frank-Cucumber (iOS) features
| guard-calabash-ios | Testing | return Calabash iOS Cucumber features
| guard-redis | Utility | restarts Redis server when needed
| guard-shopify | Web Development | automatically upload and update Shopify templates when they change
| guard-readme-on-github | Documentation | preview GitHub pages locally before pushing them to GH
| guard-rsync | Utility | automatically sync directories with RSync whenever they change
| guard-jasmine-headless-webkit | Testing | rerun Jasmine tests in a headless WebKit instance
| guard-jshint-node | Code Quality | detect errors and potential problems in JavaScript files
| guard-resque | Utility | restarts Resque workers
| guard-delayed | Utility | automatically restarts delayed_job workers
| guard-rocco | Documentation | regenerates Rocco docs
| guard-slim | Web Development | regenerate slim templates
| guard-rails_best_practices | Rails | check if code matches Rails Best Practices
| guard-gimli | Documentation | convert markup files (markdown, rdoc) into PDF files
| guard-sprite-factory | Web Development | regenerate CSS sprites from a series of images
| guard-jasmine-node | Testing | reruns Jasmine Node.js tests
| guard-post | Utility | automatically load text files into database records (Mongoid, ActiveRecord, etc.)
| guard-autorefresh | Rails | Reload the browser whenever views change |
| guard-zen | Utility | Runs Ruby Koans
| guard-premailer | Web Development | inline CSS in email templates
| guard-uglify | Web Development | compress JavaScript files using uglifier gem
| guard-jenkins | Testing | sets a Jenkins status image depending whether there's a failure or not
| guard-git-scribe | Documentation | rebuild git-scribe ebooks
| guard-flopbox | Utility | synchronize directories via SFTP
| guard-markdown | Documentation | convert Markdown files to HTML
| guard-chef | DevOps | watches and reloads Chef recipes automatically
| guard-prove | Testing | reruns Perl tests

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