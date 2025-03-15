source "https://rubygems.org"
gem 'github-pages'
gem "webrick", "~> 1.7"

# Windows and JRuby does not include zoneinfo files, so bundle the tzinfo-data gem
# and associated library.
platforms :mingw, :x64_mingw, :mswin, :jruby do
  gem "tzinfo", ">= 1", "< 3"
  gem "tzinfo-data"
end

# If having issues on windows with auto regeneration
#gem "wdm", "~> 0.1.1", :install_if => Gem.win_platform?