NOTE: Guard maintainers are not responsible for the quality or suitability of the plugins below. (Though, some plugins are maintained by Guard core developers.)

Ordering is generally by popularity/user-friendliness/completeness/support/active-development. Disputes about order should be resolved by project "star" count.

NOTE: if any plugins are broken or outdated, try the following:
1. find the gem on rubygems.org, then go to the homepage
2. file an issue there and wait up to a few days for the author to respond
3. if the plugin author isn't responding CC a Guard maintainer in the issue (e.g. me: @e2)

NOTE: some plugin authors work on their own forks instead of the forks in the Guard organization. Please update the links below if they point to the wrong/outdated fork.

## Popular / Featured / Well supported

| Plugin | When to use |
| ------ | ------------|
| [guard-bundler](https://github.com/guard/guard-bundler) | installs/updates gems when Gemfile changes
| [guard-rspec](https://rubygems.org/gems/guard-rspec) | Smart/incremental RSpec runner
| [guard-minitest](https://rubygems.org/gems/guard-minitest) | runs Minitest and Test/Unit tests
| [guard-cucumber](https://github.com/guard/guard-cucumber) |  Reruns changed/affected Cucumber Features
| [guard-zeus](https://github.com/guard/guard-zeus) |  Zeus speeds up startup time for Rails commands (development, server, testing)
| [guard-jasmine](https://github.com/guard/guard-jasmine) | Frontend testing using PhantomJS/Webkit
| [guard-cucumber](https://github.com/guard/guard-cucumber) |  Reruns changed/affected Cucumber Features
| [guard-jekyll-plus](http://github.com/imathis/guard-jekyll-plus) |  Extensive plugin for working with Jekyll projects
| [guard-brakeman](https://github.com/guard/guard-brakeman) |  Scans your Rails application for known security holes (CVE's)
| [guard-rubocop](https://github.com/yujinakayama/guard-rubocop) |  Check your source files to style violations and potential problems
| [guard-puppet](https://github.com/guard/guard-puppet) |  Helps build Puppet catalogs for deploying and managing sites and servers
| [guard-shell](http://github.com/hawx/guard-shell) |  Runs shell commands when changes happen - also supports notifications and long -running programs
| [guard-livereload](https://rubygems.org/gems/guard-livereload) | Reloads browser whenever web pages change
| [guard-nanoc](http://nanoc.ws/) | rebuild Nanoc websites
| [guard-process](https://github.com/guard/guard-process) | Manages background processes (servers, daemons)
| [guard-yield](https://github.com/guard/guard-yield) | runs any Ruby code (without the need to write a Guard plugin)
| [guard-kjell](http://github.com/magplus/guard-kjell) | runs command once when watched file changes

## Rails related

| Plugin | When to use |
| ------ | ------------|
| [guard-brakeman](https://github.com/guard/guard-brakeman) |  Scans your Rails application for known security holes (CVE's)
| [guard-migrate](https://github.com/guard/guard-migrate) |  Migrates the database whenever you add/change migrations
| [guard-jammit](http://github.com/guard/guard-jammit) |  Compressing assets (JS, CSS)
| [guard-annotate](http://craigjolicoeur.com) | Inserts "cheatsheets" about your database schema into your source files
| [guard-passenger](https://github.com/guard/guard-passenger) |  Manages the Passenger server (restarts when necessary)
| [guard-sprockets](https://github.com/guard/guard-sprockets) |  Recompiles assets using Sprockets
| [guard-cogs](https://github.com/ralfthewise/guard-cogs) | guard-sprockets alternative
| [guard-rails_best_practices](https://github.com/guard/guard-rails_best_practices) | check if code matches Rails Best Practices
| [guard-bower_rails](https://rubygems.org/gems/guard-bower_rails) | Automatically install/update Rails bower dependencies
| [guard-bundler-audit](https://github.com/christianhellsten/guard-bundler-audit) | check for gems with vulnerabilities
| [guard-consistency_fail](http://rubygems.org/gems/guard-consistency_fail) | detect missing unique indexes in Rails projects
| [guard-flow](https://github.com/blainekasten/guard-flow) | runs flow type checker on Rails javascript files

## Website generating/authoring

| Plugin | When to use |
| ------ | ------------|
| [guard-jekyll-plus](http://github.com/imathis/guard-jekyll-plus) |  Extensive plugin for working with Jekyll projects
| [guard-middleman](https://github.com/guard/guard-middleman) |  Rebuilds Middleman static websites
| [guard-nanoc](http://nanoc.ws/) | rebuild Nanoc websites

## Web CSS/template processing/compiling

| [guard-coffeescript](https://github.com/guard/guard-coffeescript) |  Compiles CoffeeScript files
| [guard-compass](https://github.com/guard/guard-compass) |  Rebuilds your CSS files in Compass Sass projects
| [guard-tilt](http://github.com/boof/guard-tilt) |?
| [guard-sass](https://github.com/guard/guard-sass) |  Recompiles Sass files to CSS
| [guard-slim](https://github.com/guard/guard-slim) |  regenerate slim templates
| [guard-haml](https://github.org/guard/guard-haml) | compile Haml templates to HTML
| [guard-less](https://rubygems.org/gems/guard-less) | compile LESS templates
| [guard-stylus](https://github.com/TimDumol/guard-stylus) | compile Node.js Stylus CSS templates
| [guard-erb](https://github.com/omarramos/guard-erb) | compiles erb files
| [guard-haml-coffee](https://github.com/ouvrages/guard-haml-coffee) | compiles HamlCoffe templates to JavaScript
| [guard-herbalizer](https://github.com/ouvrages/guard-herbalizer) | converts Haml to Erb using herbalizer
| [guard-hogan](http://github.com/fullsailor/guard-hogan) | compiles hogan mustache templates
| [guard-jade](https://github.com/TimDumol/guard-jade) | compile Jade files


## General Web Development

| Plugin | When to use |
| ------ | ------------|
| [guard-livereload](https://rubygems.org/gems/guard-livereload) | Reloads browser whenever web pages change
| [guard-embertools](https://github.com/wbhumphrey/guard-embertools) | rebuilds application.js when ember files are modified
| [guard-pusher](http://github.com/carhartl/guard-pusher) |  Send messages to multiple iPad/iPhone browsers (like "reload page")
| [guard-shopify](https://github.com/guard/guard-shopify) |  automatically upload and update Shopify templates when they change
| [guard-premailer](https://github.com/guard/guard-premailer) |  inline CSS in email templates
| [guard-sprite-factory](https://github.com/guard/guard-sprite-factory) | Web Development | regenerate CSS sprites from a series of images
| [guard-i18n-js](http://rubygems.org/gems/guard-i18n-js) | export i18n js tranlations

### Restarting servers/daemons/workers

| Plugin | When to use |
| ------ | ------------|
| [guard-process](https://github.com/guard/guard-process) | Manages background processes (servers, daemons)
| [guard-redis](https://github.com/guard/guard-redis) |  restarts Redis server when needed
| [guard-go](https://github.com/guard/guard-go) |  Run and restart go programs and servers when changed
| [guard-resque](http://github.com/railsjedi/guard-resque) |  restarts Resque workers
| [guard-delayed](https://github.com/guard/guard-delayed) |  automatically restarts delayed_job workers
| [guard-webrick](https://github.com/guard/guard-webrick) |  Restarts WEBrick server when needed
| [guard-rack](https://github.com/dblock/guard-rack) | restarts Rack app server
| [guard-puma](https://github.com/jc00ke/guard-puma) | restarts Puma app server
| [guard-foreman](https://github.com/J3RN/guard-foreman) | reruns foreman
| [guard-goliath](https://github.com/duderman/guard-goliath) | restarts Goliath apps
| [guard-grunt](http://rubygems.org/gems/guard-grunt) | restarts Grunt
| [guard-gulp](http://rubygems.org/gems/guard-gulp) | restarts Gulp

## Web asset optimization

| Plugin | When to use |
| ------ | ------------|
| [guard-uglify](http://aaroncruz.com) |  compress JavaScript files using uglifier gem
| [guard-steering](https://github.com/guard/guard-steering) |  Speed up Handlebar.js templates by precompiling them
| [guard-concat](http://github.com/makevoid/guard-concat) | concat assets (JS/CSS) into single files
| [guard-image_optim](http://github.com/ezekg/guard-image_optim) | optimizes images with image_optim
| [guard-imageoptim](https://github.com/rjocoleman/guard-imageoptim/) | optimze images with ImageOptim-CLI

## Testing

| Plugin | When to use |
| ------ | ------------|
| [guard-cucumber](https://github.com/guard/guard-cucumber) |  Reruns changed/affected Cucumber Features
| [guard-rspec](https://rubygems.org/gems/guard-rspec) | Smart/incremental RSpec runner
| [guard-minitest](https://rubygems.org/gems/guard-minitest) | runs Minitest and Test/Unit tests
| [guard-jasmine](https://github.com/guard/guard-jasmine) | Frontend testing using PhantomJS/Webkit
| [guard-teaspoon](https://github.com/guard/guard-teaspoon) |  Web testing with PhantomJS or Selenium WebDriver
| [guard-prove](https://github.com/guard/guard-prove) |  reruns Perl tests
| [guard-motion](https://github.com/guard/guard-motion) |  reruns specs for RubyMotion (iOS, Android, OSX Ruby apps)
| [guard-phpunit](https://github.com/guard/guard-phpunit) |  Guard::PHPUnit automatically runs your tests
| [guard-frank](https://github.com/AlexDenisov/guard-frank) |  rerun Frank-Cucumber (iOS) features
| [guard-calabash-ios](https://github.com/AlexDenisov/guard-calabash-ios) |  return Calabash iOS Cucumber features
| [guard-jasmine-headless-webkit](https://github.com/guard/guard-jasmine-headless-webkit) |  rerun Jasmine tests in a headless WebKit instance
| [guard-jasmine-node](https://github.com/kapoq/guard-jasmine-node) |  reruns Jasmine Node.js tests
| [guard-jenkins](https://github.com/guard/guard-jenkins) |  sets a Jenkins status image depending whether there's a failure or not
| [guard-bdd](http://github.com/nistude/guard-bdd) | run tests in order: unit tests, integration tests, then acceptance tests
| [guard-cedar](https://github.com/ohrite/guard-cedar) | runs Cedar (Objective-C) BDD tests
| [guard-codeception](https://github.com/colby-swandale/guard-codeception) | run Codeception tests (PHP)
| [guard-combustion](http://github.com/Chosko/guard-combustion) | testing Rails Engines
| [guard-cunit](http://teacup-on-rockingchair.github.com/guard-cunit/)| run CUnit tests
| [guard-elixir](https://github.com/webcoyote/guard-elixir) | runs Elixir tests using "mix test"
| [guard-gotest](https://github.com/hatoishi/guard-gotest) | runs Go tests
| [guard-gradle](https://github.com/bricker/guard-gradle) | builds and runs Java tests (Gradle projects)
| [guard-gradle-android-test](https://github.com/STAR-ZERO/guard-gradle-android-test) | runs Java Gradle tests for Android
| [guard-java](http://github.com/infospace/guard-java) | run tests in Java (using Ant or shell) + Android support
| [guard-haskell](https://github.com/supki/guard-haskell#readme) | runs Haskell specs
| [guard-jaspec](https://github.com/gisikw/guard-jaspec) | run Jaspec JavaScript files
| [guard-jessie](https://github.com/mehowte/guard-jessie) | Jasmine runner using Node.js Jessie runner
| [guard-jruby-minitest](https://github.com/jackxxu/guard-jruby-minitest) | no-startup-code JRuby Minitest test reloader
| [guard-jruby-rspec](http://rubygems.org/gems/guard-jruby-rspec) | keeps a JVM warmed up for your specs
| [guard-julia](https://github.com/svs14/guard-julia) | runs Julia tests
| [guard-karma](https://github.com/lesniakania/guard-karma) | runs the Karma JS test runner
| [guard-konacha](https://github.com/alexgb/guard-konacha) | runs Konacha (mocha + chai) JavaScript tests on Rails apps

### Code Quality
| Plugin | When to use |
| ------ | ------------|
| [guard-cane](https://github.com/guard/guard-cane) |  fails the build if your source files fail the quality level
| [guard-rubocop](https://github.com/guard/guard-rubocop) |  Check your source files to style violations and potential problems
| [guard-jshint-node](http://github.com/pahen/guard-jshint-node) |  detect errors and potential problems in JavaScript files
| [guard-coffeelint](http://github.com/meagar/guard-coffeelint) | run coffeelint
| [guard-flog](https://github.com/pericles/guard-flog/) | creates flog reports
| [guard-jshint-on-rails](https://github.com/MrOrz/guard-jshint-on-rails) | uses jshint on Rails project
| [guard-jslint](https://github.com/thelazycamel/guard-jslint) | runs jslint on JavaScript files

### Documentation
| Plugin | When to use |
| ------ | ------------|
| [guard-hologram](https://github.com/kmayer/guard-hologram) |  generates beautiful style guides for CSS
| [guard-docbook-status](https://github.com/rvolz/guard-docbook-status/) |  update docbook document overviews (structure stats)
| [guard-readme-on-github](https://github.com/listrophy/guard-readme-on-github) |  preview GitHub pages locally before pushing them to GH
| [guard-rocco](https://github.com/guard/guard-rocco) |  regenerates Rocco docs
| [guard-gimli](https://github.com/walle/guard-gimli) |  convert markup files (markdown, rdoc) into PDF files
| [guard-git-scribe](https://github.com/jasonm/guard-git-scribe) |  rebuild git-scribe ebooks
| [guard-markdown](https://github.com/guard/guard-markdown) |  convert Markdown files to HTML
| [guard-ronn](https://rubygems.org/gems/guard-ronn) | compile man pages
| [guard-inch](https://github.com/chills42/guard-inch) | documentation measurement tool for Ruby

### Deploying / DevOps / System services

| Plugin | When to use |
| ------ | ------------|
| [guard-s3](https://github.com/guard/guard-s3) |  Synchronize folders with Amazon S3 buckets
| [guard-puppet](https://github.com/guard/guard-puppet) |  Helps build Puppet catalogs for deploying and managing sites and servers
| [guard-chef](http://rubygems.org/gems/guard-chef) |  watches and reloads Chef recipes automatically
| [guard-flopbox](http://github.com/vincentchu/guard-flopbox) | synchronize directories via SFTP
| [guard-autoupload](https://github.com/jyrkij/guard-autoupload) | upload files using SFTP or FTP
| [guard-bosh](https://github.com/cloudcredo/guard-bosh) | update Cloud Foundry BOSH config (large scale distributed services)
| [guard-clockwork](https://github.com/deepblue/guard-clockwork) | restart Clockwork instances (Clockwork = Cron replacement written)
| [guard-fig](https://rubygems.org/gems/guard-fig) | help develop docker containers using fig
| [guard-foodcritic](https://github.com/Nordstrom/guard-foodcritic) | lint tool for Opscode Chef cookbooks
| [guard-kitchen](http://github.com/opscode/guard-kitchen) | use Kitchen to develop Chef cookbooks
| [guard-knife](https://github.com/nistude/guard-knife) | update Chef cookbooks, data bags, envs and roles automatically

### Editor helpers (ctags generators)

| Plugin | When to use |
| ------ | ------------|
| [guard-ctags-bundler](https://github.com/ivalkeen/guard-ctags-bundler) |  regenerates CTags files so editors can find method definitions
| [guard-ctags-composer](https://github.com/everzet/guard-ctags-composer) | for PHP projects

### Utility

| Plugin | When to use |
| ------ | ------------|
| [guard-bundler](https://github.com/guard/guard-bundler) | installs/updates gems when Gemfile changes
| [guard-shell](https://github.com/guard/guard-shell) |  Runs shell commands when changes happen - also supports notifications and long -running programs
| [guard-yield](https://github.com/guard/guard-yield) | runs any Ruby code (without the need to write a Guard plugin)
| [guard-rake](http://github.com/rubyist/guard-rake) |  reruns a rake task when files change
| [guard-rsync](http://github.com/kselden/guard-rsync) |  automatically sync directories with RSync whenever they change
| [guard-post](http://github.com/viatropos/guard-post) |  automatically load text files into database records (Mongoid, ActiveRecord, etc.)
| [guard-lilypond](https://github.com/guard/guard-lilypond) | Engraving music scores
| [guard-zen](http://iscra.co.uk) |  Runs Ruby Koans
| [guard-blogger](https://github.com/scottatron/guard-blogger) | update Blogger templates
| [guard-cocoapods](https://github.com/kreeger/guard-cocoapods) | installs CocoaPods
| [guard-bundler](https://github.com/guard/guard-bundler) | installs/updates gems when Gemfile changes
| [guard-copy](https://github.com/marcisme/guard-copy) | copy files whenever files are created or modified
| [guard-copy3](https://github.com/mattjorn/guard-copy3) | copies files and folders whenever files are created or modified
| [guard-entangle](http://rubygems.org/gems/guard-entangle) | expands files inline
| [guard-gitpusher](https://github.com/hatone/guard-gitpusher) | automatically uploads changed files to Git repository


### Guard Plugin development

| Plugin | When to use |
| ------ | ------------|
| [guard-compat](https://github.com/guard/guard-compat) | Essential for developing and testing Guard Plugins
| [guard-yield](https://github.com/guard/guard-yield) | runs any Ruby code (without the need to write a Guard plugin)
| [guard-helpers](https://github.com/TimDumol/guard-helpers) | helpers modules for Guard plugins

### Not yet categorized/described

NOTE: I (@e2) haven't gone through these - please move these into the above categories if any are usable/useful enough:

| Plugin | When to use |
| ------ | ------------|
| [guard-addremove](http://github.com/pehlert/guard-addremove) | ?
| [guard-asciidoctor]: | ?
| [guard-bacon]: | ?
| [guard-blink1](https://github.com/GeoffTidey/guard-blink1) |?
| [guard-bower]: |?
| [guard-catalog](https://github.com/garno/guard-catalog) |?
| [guard-cloudformation]: |?
| [guard-concatfilter](http://github.com/geoffyoungs/guard-concat) |?
| guard-cop: |?
| [guard-cucumber-js]: |?
| [guard-depend](http://grossweber.com) |?
| [guard-ecukes](http://github.com/dillonkearns/guard-ecukes) |?
| [guard-ejs]: |?
| [guard-erlang](http://github.com/hpyhacking/guard-erlang) |?
| [guard-evergreen](https://github.com/criticalpair/guard-evergreen) |?
| [guard-faye](http://github.com/d4rk5eed/guard-faye) |?
| [guard-fixture_builder]: |?
| [guard-flay]: |?
| [guard-go]: |?
| [guard-haml-ext]: |?
| [guard-haml2erb]: |?
| [guard-handlebars](http://labs.thredup.com) |?
| [guard-i18next]: |?
| [guard-jasmine-rails]: |?
| [guard-jenkins](http://justinstoller.github.com/guard-jenkins) |?
| [guard-jet](http://github.com/erwanb/guard-gem) |?
| [guard-jetty]: |?
| [guard-js-static-require]: |?
| [guard-jshintrb]: |?
| [guard-jslint-on-rails]: |?
| [guard-jslint-on-rails-for-1.1.1]: |?
| [guard-jst]: |?
| [guard-koans]: |?
| [guard-konacha-rails](https://github.com/lbeder/guard-konacha-rails) |?
| [guard-konacha-version](https://github.com/lbeder/guard-konacha-rails) |?
| [guard-lessc](https://github.com/cavneb/guard-lessc) |?
| [guard-librarian](http://rubygems.org/gems/guard-librarian) |?
| [guard-live-set](http://github.com/mgarriss/guard-live-set) |?
| [guard-llsprockets](https://github.com/LivingLogic/guard-llsprockets) |?
| [guard-lono]: |?
| [guard-markdown](https://github.com/darwalenator/guard-markdown) |?
| [guard-markdown2impress](http://rubygems.org/gems/guard-markdown2impress) |?
| [guard-maven](https://github.com/jhubert/guard-maven) |?
| [guard-minitest-decisiv](http://github.com/DecisivInc/guard-minitest) |?
| [guard-mirror](https://github.com/caseywebdev/guard-mirror) |?
| [guard-mocha-node](https://github.com/neerolyte/guard-mocha-node) |?
| [guard-mouch](https://github.com/semanticdreamer/guard-mouch) |?
| [guard-mthaml](http://github.com/ezekg/guard-mthaml) |?
| [guard-mustachejs](https://github.com/jamiew/guard-mustachejs) |?
| [guard-mutant](https://github.com/yujinakayama/guard-rubocop) |?
| [guard-notifier-blink1](https://github.com/Sixeight/guard-notifier-blink1) |?
| [guard-notifier-git_auto_commit]: |?
| [guard-notifier-gntp_only-darwin](https://github.com/mmichaa/guard-notifier-gntp_only-darwin) |?
| [guard-npm](http://rubygems.org/gems/guard-npm) |?
| [guard-ocunit](https://github.com/ap4y/guard-ocunit) |?
| [guard-opal-rails]: |?
| [guard-openscad](http://github.com/cpb/guard-openscad) |?
| [guard-parallel_all](https://github.com/answer/guard-parallel_all) |?
| [guard-pdflatex](http://github.com/jimjh/guard-pdflatex) |?
| [guard-phantomjs-jasmine](http://github.com/stas/guard-phantomjs-jasmine) |?
| [guard-phpcs](http://github.com/EricHogue/guard-phpcs) |?
| [guard-phpmd](http://github.com/EricHogue/guard-phpmd) |?
| [guard-phpspec](http://github.com/lsd/guard-phpspec) |?
| [guard-phpunit2]: |?
| [guard-play](http://github.com/crazycode/guard-play) |?
| [guard-pow](http://rubygems.org/gems/guard-pow) |?
| [guard-predictionio](https://rubygems.org/RootsRated/guard-predictionio) |?
| [guard-preek]: |?
| [guard-preserves]: |?
| [guard-processing](http://github.com/y310/guard-processing) |?
| [guard-prostores]: |?
| [guard-puppet-lint](http://github.com/alister/guard-puppet-lint) |?
| [guard-pushover](https://github.com/joenas/guard-pushover/) |?
| [guard-pytest](https://github.com/kazufusa/guard-pytest) |?
| [guard-python-unittest]: |?
| [guard-rackunit](https://github.com/neomantic/guard-rackunit) |?
| [guard-rackup]: |?
| [guard-ragel](https://github.com/excepttheweasel/guard-ragel) |?
| [guard-rails](https://github.com/ranmocy/guard-rails) |?
| [guard-rails_best_practices](http://rubygems.org/gems/guard-rails_best_practices) |?
| [guard-railsbp](https://github.com/andreygerasimchuk/guard-railsbp) |?
| [guard-railstestdb](https://github.com/singlebrook/guard-railstestdb) |?
| [guard-rake-vagrant](https://github.com/afiune/guard-rake-vagrant) |?
| [guard-rdoc](https://github.com/bspaulding/guard-rdoc) |?
| [guard-rebar](http://github.com/andrzejsliwa/guard-rebar) |?
| [guard-redcarpet](https://github.com/SegFaultAX/guard-redcarpet) |?
| [guard-reek](https://github.com/gvillalta99/guard-reek) |?
| [guard-reloader](https://github.com/fajarmf/Rails-Autotester) |?
| [guard-remote-sync](https://github.com/pmcjury/guard-remote-sync) |?
| [guard-resque-scheduler](http://github.com/dlnichols/guard-resque-scheduler) |?
| [guard-restarter](https://github.com/cespare/guard-restarter) |?
| [guard-rna]: |?
| [guard-roxy](https://github.com/paxtonhare/guard-roxy) |?
| [guard-rrails](http://github.com/walf443/guard-rrails) |?
| [guard-rspec-jruby](http://github.com/garrettheaver/guard-rspec-jruby) |?
| [guard-rubby](http://rubby-lang.org/) |?
| [guard-ruby]: |?
| [guard-rubybeautify](https://github.com/erniebrodeur/guard-rubybeautify) |?
| [guard-rubycritic](https://github.com/whitesmith/guard-rubycritic) |?
| [guard-rust]: |?
| [guard-schema](https://github.com/icrowley/guard-schema) |?
| [guard-schema](https://github.com/icrowley/guard-schema) |?
| [guard-sculpin](http://github.com/florianeckerstorfer/guard-sculpin) |?
| [guard-seeds](https://github.com/icrowley/guard-seeds) |?
| [guard-shellexec]: |?
| [guard-shopify](https://github.com/1337807/guard-shopify) |?
| [guard-shopifytheme](http://github.com/dannysmith/guard-shopifytheme) |?
| [guard-shoryuken](http://github.com/tagloo/guard-shoryuken) |?
| [guard-shotgun](http://github.com/rchampourlier/guard-shotgun) |?
| [guard-sidekiq](http://github.com/uken/guard-sidekiq) |?
| [guard-simple_shell]: |?
| [guard-spin](http://github.com/vizjerai/guard-spin) |?
| [guard-spinach](http://github.com/codegram/guard-spinach) |?
| [guard-spinoff](https://github.com/bernd/guard-spinoff) |?
| [guard-spork](http://rubygems.org/gems/guard-spork) |?
| [guard-sporkminitest](https://github.com/rking/guard-minitest) |?
| [guard-spring](https://github.com/mknapik/guard-spring) |?
| [guard-sprite-factory](http://chrishein.com) |?
| [guard-sprockets2](https://github.com/stevehodgkiss/guard-sprockets2) |?
| [guard-staticmatic](https://github.com/mihar/guard-staticmatic) |?
| [guard-steering](https://github.com/ustwo/guard-steering) |?
| [guard-stitch]: |?
| [guard-stitch-plus](https://github.com/imathis/guard-stitch-plus) |?
| [guard-strainer](https://github.com/wingrunr21/guard-strainer) |?
| [guard-sublime-ctags](https://github.com/sunteya/guard-sublime-ctags) |?
| [guard-sunspot](http://github.com/anthonator/guard-sunspot) |?
| [guard-sync]: |?
| [guard-tap](http://github.com/hitode909/guard-tap) |?
| [guard-tay](http://github.com/rixth/guard-tay) |?
| [guard-teabag](https://github.com/modeset/guard-teabag) |?
| [guard-templates]: |?
| [guard-templates-jshaml](https://github.com/sdrdis/guard-templates-jshaml/) |?
| [guard-test](https://rubygems.org/gems/guard-test) |?
| [guard-tishadow](http://github.com/ijcd/guard-tishadow) |?
| [guard-titan](https://github.com/dcunited001/guard-titan) |?
| [guard-toc](https://github.com/j2fly/guard-toc) |?
| [guard-treetop](https://github.org/rizzatti/guard-treetop) |?
| [guard-typescript](http://github.com/jabbawookiees/guard-typescript) |?
| [guard-unicorn](https://github.com/xhr/guard-unicorn) |?
| [guard-unity](https://github.com/rubyrainbows/guard-unity-test) |?
| [guard-vows](https://github.com/jamesotron/guard-vows) |?
| [guard-webhook-notifier](https://github.com/yuku-t/guard-webhook-notifier) |?
| [guard-webpack](https://github.com/gisikw/guard-webpack) |?
| [guard-xcode](https://github.com/kisom/guard-xcode) |?
| [guard-xcoder](http://github.com/burtlo/guard-xcoder) |?
| [guard-xctool-test](https://github.com/siuying/guard-xctool-test) |?
| [guard-yaml](https://github.com/philtr/guard-yaml) |?
| [guard-yamlsort](http://vendetta.io) |?
| [guard-yard](https://github.com/panthomakos/guard-yard) |?
| [guard-yardstick]: |?
| [guard-yeti](https://github.com/hojberg/guard-yeti) |?
| [guard-zeus-client](https://github.com/aceofsales/guard-zeus-client) |?
| [guard-zeus_server]: |?

### Outdated/Obsolete plugins

| Outdated Plugin | Why outdated/obsolete |
| ------ | -------- |
| [Rails-Autotester](https://github.com/guard/Rails-Autotester) | probably replaced with Guard::Minitest
| [guard-autorefresh](https://github.com/guard/guard-autorefresh) | superseeded by Guard::LiveReload
| [guard-coffeedripper](http://github.com/amacou/guard-coffeedripper) | probably outdated
| [guard-db](https://github.com/guard/guard-db) | probably replaced with guard-migrate
| [guard-ego](https://github.com/guard/guard-ego) | Guard can now reload itself
| [guard-focus](http://github.com/supaspoida/guard-focus) | probably can be replaces with Guard::RSpec with custom config
| [guard-hydra](https://github.com/guard/guard-hydra) | probably replaced with Guard::RSpec using parallel specs (check Guard::RSpec Readme)
| [guard-jekyll](http://davidhaslem.com) | superseeded by guard-jekyll-plus
| [guard-jessie](https://github.com/guard/guard-jessie) | likely superseeded by guard-jasmine
| [guard-jslint-on-rails](https://github.com/guard/guard-jslint-on-rails) | probably outdated
| [guard-jstd](https://github.com/arailsdemo/guard-jstd) | probably superseeded by other JavaScript testing Guard plugins
| [guard-krl](http://code.kynetx.com) | updates cloud-based Kinetic Rules Engine rule files (company dissolved)
| [guard-mozrepl](http://branch14.org/guard-mozrepl) | probably superseeded by Guard::LiveReload
| [guard-phantomjs](https://github.com/guard/guard-phantomjs) | probably superseeded by other JavaScript testing Guard plugins
| [guard-rails-assets](https://github.com/guard/guard-rails-assets) | not sure if it works with Rails 4
| [guard-rspectacle](https://github.com/guard/guard-rspectacle) | Embedded RSpec runner - probably better to use Guard::Rspec or Guard::Zeus
| [guard-soca](http://github.com/rubbish/guard-soca) | likely outdated
| [guard-spring](https://github.com/guard/guard-spring) | guard-rspec supports running RSpec with Spring and a lot more
| [guard-sprockets2](https://github.com/guard/guard-sprockets2) | probably outdated
| [guard-stendhal](https://github.com/guard/guard-stendhal) | likely outdated
| [guard-stitch](https://github.com/guard/guard-stitch) | alternative to guard-sprockets, but may be outdated
| [guard-jekyll2] | probably replaced with guard-jekyll-plus
| [guard-fast_spec](http://rubygems.org/gems/guard-fast_spec) | probably obsolete
