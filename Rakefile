desc "Bump Gem Version, Build Gem, and Upload to Gemfury"
task :deploy do
  version = File.open("VERSION").read.strip.gsub(/\.[0-9]*$/, ".#{Time.now.to_i}")
  gemfile = "mini_record_safe-#{version}.gem"
  gemspec = "mini_record_safe.gemspec"

  gemspec_contents = File.open(gemspec).read.gsub(/\.version = .*$/, ".version = '#{version}'")
  File.open(gemspec, "w") { |f| f.write(gemspec_contents) }
  File.open("VERSION", "w") { |f| f.write(version) }

  `gem build mini_record_safe.gemspec`
  `curl -F p1=@#{gemfile} https://gems.gemfury.com/cgSsDV8i4yL4mnuN8zk7/`
  `rm #{gemfile}`
end

