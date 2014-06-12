desc "Bump Gem Version, Build Gem, and Upload to Gemfury"
task :deploy do
  old_version = File.open("VERSION").read.strip.split(".")
  old_version.push(old_version.pop.to_i + 1)
  version = old_version.join(".")
  ["mini_record_safe"].each do |ver|
    puts "Deploying #{ver}"
    gemfile = "#{ver}-#{version}.gem"
    gemspec = "#{ver}.gemspec"

    gemspec_contents = File.open(gemspec).read.gsub(/\.version = .*$/, ".version = '#{version}'")
    File.open(gemspec, "w") { |f| f.write(gemspec_contents) }
    File.open("VERSION", "w") { |f| f.write(version) }

    sh "gem build #{gemspec}"
    sh "curl -D- -F package=@#{gemfile} https://push.fury.io/cgSsDV8i4yL4mnuN8zk7/"
    sh "rm #{gemfile}"
  end
end
