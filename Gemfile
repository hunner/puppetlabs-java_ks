#This file is generated by ModuleSync, do not edit.

source ENV['GEM_SOURCE'] || "https://rubygems.org"

# Determines what type of gem is requested based on place_or_version.
def gem_type(place_or_version)
  if place_or_version =~ /^git:/
    :git
  elsif place_or_version =~ /^file:/
    :file
  else
    :gem
  end
end

# Find a location or specific version for a gem. place_or_version can be a
# version, which is most often used. It can also be git, which is specified as
# `git://somewhere.git#branch`. You can also use a file source location, which
# is specified as `file://some/location/on/disk`.
def location_for(place_or_version, fake_version = nil)
  if place_or_version =~ /^(git[:@][^#]*)#(.*)/
    [fake_version, { :git => $1, :branch => $2, :require => false }].compact
  elsif place_or_version =~ /^file:\/\/(.*)/
    ['>= 0', { :path => File.expand_path($1), :require => false }]
  else
    [place_or_version, { :require => false }]
  end
end

# Used for gem conditionals
ruby_version_segments = Gem::Version.new(RUBY_VERSION.dup).segments
minor_version = "#{ruby_version_segments[0]}.#{ruby_version_segments[1]}"

# The following gems are not included by default as they require DevKit on Windows.
# You should probably include them in a Gemfile.local or a ~/.gemfile
#gem 'pry' #this may already be included in the gemfile
#gem 'pry-stack_explorer', :require => false
#if RUBY_VERSION =~ /^2/
#  gem 'pry-byebug'
#else
#  gem 'pry-debugger'
#end

group :development do
  gem "puppet-module-posix-default-r#{minor_version}",    :require => false, :platforms => "ruby"
  gem "puppet-module-win-default-r#{minor_version}",      :require => false, :platforms => ["mswin", "mingw", "x64_mingw"]
  gem "puppet-module-posix-dev-r#{minor_version}",        :require => false, :platforms => "ruby"
  gem "puppet-module-win-dev-r#{minor_version}", '0.0.7', :require => false, :platforms => ["mswin", "mingw", "x64_mingw"]
  gem "json_pure", '<= 2.0.1',                            :require => false if Gem::Version.new(RUBY_VERSION.dup) < Gem::Version.new('2.0.0')
  gem "fast_gettext", '1.1.0',                            :require => false if Gem::Version.new(RUBY_VERSION.dup) < Gem::Version.new('2.1.0')
  gem "fast_gettext",                                     :require => false if Gem::Version.new(RUBY_VERSION.dup) >= Gem::Version.new('2.1.0')
  gem "github_changelog_generator", :path => '~/Documents/work/git/github-changelog-generator'
end

group :system_tests do
  gem "puppet-module-posix-system-r#{minor_version}",                            :require => false, :platforms => "ruby"
  gem "puppet-module-win-system-r#{minor_version}",                              :require => false, :platforms => ["mswin", "mingw", "x64_mingw"]
  gem "beaker", *location_for(ENV['BEAKER_VERSION'] || '>= 3')                  
  gem "beaker-pe",                                                               :require => false
  gem "beaker-rspec", *location_for(ENV['BEAKER_RSPEC_VERSION'])                
  gem "beaker-hostgenerator", *location_for(ENV['BEAKER_HOSTGENERATOR_VERSION'])
  gem "beaker-abs", *location_for(ENV['BEAKER_ABS_VERSION'] || '~> 0.1')        
end

gem 'puppet', *location_for(ENV['PUPPET_GEM_VERSION'])

# Only explicitly specify Facter/Hiera if a version has been specified.
# Otherwise it can lead to strange bundler behavior. If you are seeing weird
# gem resolution behavior, try setting `DEBUG_RESOLVER` environment variable
# to `1` and then run bundle install.
gem 'facter', *location_for(ENV['FACTER_GEM_VERSION']) if ENV['FACTER_GEM_VERSION']
gem 'hiera', *location_for(ENV['HIERA_GEM_VERSION']) if ENV['HIERA_GEM_VERSION']

if Gem::Platform.local.os == 'mingw32'
  # If we're using a Puppet gem on windows, which handles its own win32-xxx gem dependencies (Pup 3.5.0 and above), set maximum versions
  # Required due to PUP-6445
  gem "win32-dir", "<= 0.4.9",        :require => false
  gem "win32-eventlog", "<= 0.6.5",   :require => false
  gem "win32-process", "<= 0.7.5",    :require => false
  gem "win32-security", "<= 0.2.5",   :require => false
  gem "win32-service", "<= 0.8.8",    :require => false
end

# Evaluate Gemfile.local if it exists
if File.exists? "#{__FILE__}.local"
  eval(File.read("#{__FILE__}.local"), binding)
end

# Evaluate ~/.gemfile if it exists
if File.exists?(File.join(Dir.home, '.gemfile'))
  eval(File.read(File.join(Dir.home, '.gemfile')), binding)
end

# vim:ft=ruby
