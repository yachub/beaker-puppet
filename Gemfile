source ENV['GEM_SOURCE'] || "https://rubygems.org"

gemspec

def location_for(place, fake_version = nil)
  if place.is_a?(String) && place =~ /^(git:[^#]*)#(.*)/
    [fake_version, { :git => $1, :branch => $2, :require => false }].compact
  elsif place.is_a?(String) && place =~ /^file:\/\/(.*)/
    ['>= 0', { :path => File.expand_path($1), :require => false }]
  else
    [place, { :require => false }]
  end
end

 group :rubocop do
  gem 'rubocop', '~> 1.12.0'
  gem 'rubocop-performance'
  gem 'rubocop-rake'
  gem 'rubocop-rspec'
end

group :test do
  gem "beaker", *location_for(ENV['BEAKER_VERSION'] || ['>= 4.30.0', '< 5.0.0'])
  gem "beaker-abs", *location_for(ENV['ABS_VERSION'] || '~> 0.4.0')
end

group :release do
  gem 'github_changelog_generator', require: false
end

group :coverage, optional: ENV['COVERAGE']!='yes' do
  gem 'codecov', :require => false
  gem 'simplecov-console', :require => false
end
