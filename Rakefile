# frozen_string_literal: true

require "bundler/gem_tasks"

require 'rake/testtask'

Rake::TestTask.new do |t|
  t.libs << 'test'
  t.pattern = "{test,#{File.join(Gem.loaded_specs['kaminari-core'].gem_dir, 'test')}}/**/*_test.rb"
  t.warning = true
  t.verbose = true
end

task :install_tasks_for_sub_gems do
  Bundler::GemHelper.install_tasks dir: File.join(__dir__, 'kaminari-core'), name: 'kaminari-core'
  Bundler::GemHelper.install_tasks dir: File.join(__dir__, 'kaminari-actionview'), name: 'kaminari-actionview'
  Bundler::GemHelper.install_tasks dir: File.join(__dir__, 'kaminari-activerecord'), name: 'kaminari-activerecord'
end

Rake::Task[:build].enhance [:install_tasks_for_sub_gems]

begin
  require 'rdoc/task'

  Rake::RDocTask.new do |rdoc|
    require 'kaminari/version'

    rdoc.rdoc_dir = 'rdoc'
    rdoc.title = "kaminari #{Kaminari::VERSION}"
    rdoc.rdoc_files.include('lib/**/*.rb')
  end
rescue LoadError
  puts 'RDocTask is not supported on this VM and platform combination.'
end
