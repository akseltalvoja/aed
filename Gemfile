source "https://rubygems.org"

# Update Jekyll to a version compatible with Ruby 3+
gem "jekyll", "~> 4.3"

# Plugins
group :jekyll_plugins do
  gem "jekyll-feed", "~> 0.12"
  gem "jekyll-tidy"
end

# Windows specific timezone logic
install_if -> { RUBY_PLATFORM =~ %r!mingw|mswin|java! } do
  gem "tzinfo", "~> 1.2"
  gem "tzinfo-data"
end

# FIX: Changed "~> 0.1.1" to ">= 0.1.1" to allow newer versions that work on Ruby 3.4
gem "wdm", ">= 0.1.1", :install_if => Gem.win_platform?

gem 'jekyll-sitemap'
gem 'kramdown-math-katex'

# Required for Ruby 3.0+
gem "webrick", "~> 1.7"