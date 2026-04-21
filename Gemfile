source "https://rubygems.org"

# GitHub Pages-compatible Jekyll stack (locks Jekyll + plugins to what GitHub
# actually builds with). Keeps local previews in sync with the deployed site.
gem "github-pages", group: :jekyll_plugins

# Windows / JRuby timezone data
platforms :mingw, :x64_mingw, :mswin, :jruby do
  gem "tzinfo", ">= 1", "< 3"
  gem "tzinfo-data"
end

gem "wdm", "~> 0.1.1", :platforms => [:mingw, :x64_mingw, :mswin]
