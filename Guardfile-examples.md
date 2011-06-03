Typical Rails Guardfile with RSpec

```ruby
guard 'bundler' do
  watch('Gemfile')
end

guard 'passenger' do
  watch(%r{lib/.*\.rb$})
  watch(%r{config/.*\.rb$})
end

guard 'livereload' do
  watch(%r{^app/.+\.(erb|haml)$})
  watch(%r{^app/helpers/.+\.rb$})
  watch(%r{^/public/.+\.(css|js|html)$})
  watch(%r{^config/locales/.+\.ym$})
end

guard 'rspec', :version => 2, :bundler => false, :formatter => "instafail" do
  watch(%r{^spec/(.*)_spec\.rb$})
  watch(%r{^app/(.*)\.rb$})                          { |m| "spec/#{m[1]}_spec.rb" }
  watch(%r{^lib/(.*)\.rb$})                          { |m| "spec/lib/#{m[1]}_spec.rb" }
  watch('config/routes.rb')                          { "spec/routing" }
  watch('app/controllers/application_controller.rb') { "spec/controllers" }
  watch('spec/support/controller_spec_helpers.rb')   { "spec/controllers" }
  watch('spec/factories.rb')                         { "spec/models" }
  watch('spec/spec_helper.rb')                       { "spec" }
end
```