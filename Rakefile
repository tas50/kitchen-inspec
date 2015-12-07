# -*- encoding: utf-8 -*-

require "bundler/gem_tasks"

require "rspec/core/rake_task"
RSpec::Core::RakeTask.new(:spec)

desc "Run all test suites"
task :test => [:spec]

task :default => :spec

require "cane/rake_task"
desc "Run cane to check quality metrics"
Cane::RakeTask.new do |cane|
  cane.canefile = "./.cane"
end

require "finstyle"
require "rubocop/rake_task"
RuboCop::RakeTask.new(:style) do |task|
  task.options << "--display-cop-names"
end

desc "Display LOC stats"
task :stats do
  puts "\n## Production Code Stats"
  sh "countloc -r lib/kitchen"
  puts "\n## Test Code Stats"
  sh "countloc -r spec"
end

desc "Run all quality tasks"
task :quality => [:cane, :style, :stats]

task :default => [:test, :quality]

# Automatically generate a changelog for this project. Only loaded if
# the necessary gem is installed.
begin
  require 'github_changelog_generator/task'
  GitHubChangelogGenerator::RakeTask.new :changelog
rescue LoadError
  puts '>>>>> GitHub Changelog Generator not loaded, omitting tasks'
end
