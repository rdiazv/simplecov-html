require 'bundler'
Bundler::GemHelper.install_tasks

# See https://github.com/colszowka/simplecov/issues/171
desc "Set permissions on all files so they are compatible with both user-local and system-wide installs"
task :fix_permissions do
  system 'bash -c "find . -type f -exec chmod 644 {} \; && find . -type d -exec chmod 755 {} \;"'
end
# Enforce proper permissions on each build
Rake::Task[:build].prerequisites.unshift :fix_permissions

require 'rake/testtask'
Rake::TestTask.new(:test) do |test|
  test.libs << 'lib' << 'test'
  test.pattern = 'test/**/test_*.rb'
  test.verbose = true
end

task :default => :test

namespace :assets do
  desc "Compiles all assets"
  task :compile do
    puts "Compiling assets"
    require 'sprockets'
    assets = Sprockets::Environment.new('.')
    assets.append_path 'assets/javascripts'
    assets.append_path 'assets/stylesheets'
    assets.append_path 'assets/fonts'
    assets['application.js'].write_to('public/js/application.js')
    assets['application.css'].write_to('public/css/application.css')
    assets['fontawesome-webfont.eot'].write_to('public/fonts/fontawesome-webfont.eot')
    assets['fontawesome-webfont.svg'].write_to('public/fonts/fontawesome-webfont.svg')
    assets['fontawesome-webfont.ttf'].write_to('public/fonts/fontawesome-webfont.ttf')
    assets['fontawesome-webfont.woff'].write_to('public/fonts/fontawesome-webfont.woff')
    assets['FontAwesome.otf'].write_to('public/fonts/FontAwesome.otf')
  end
end
