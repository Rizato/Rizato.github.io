source "https://rubygems.org"

gem "jekyll", "~> 4.3"
gem "webrick" # Required for Ruby 3.0+

group :jekyll_plugins do
  gem "jekyll-feed"
  gem "jekyll-seo-tag"
  gem "jekyll-sitemap"
end

# Windows and JRuby does not include zoneinfo files
platforms :mingw, :x64_mingw, :mswin, :jruby do
  gem "tzinfo", ">= 1", "< 3"
  gem "tzinfo-data"
end

