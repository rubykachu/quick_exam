require "bundler/gem_tasks"
require "quick_exam/version"

namespace :gem do
  task :uninstall do
    uninstall_gem
    p 'Uninstalled :)'
  end

  task :reinstall do
    uninstall_gem
    remove_pkg_gem
    build_gem
    install_gem
    p 'Reinstalled :)'
  end

  task :push do
    p 'Pushed :)' if push_gem_to_remote
  end

  task :remove do |t, v|
    version = ENV['VERSION'].nil? ? QuickExam::VERSION : ENV['VERSION']
    p 'Removed :)' if remove_gem_from_remote(version)
  end

  private

  def gem_installed?
    `gem list -i quick_exam`
  end

  def pkg_gem?
    File.exists?("./quick_exam-#{QuickExam::VERSION}.gem")
  end

  def uninstall_gem
    exec 'gem uninstall quick_exam' if gem_installed?
  rescue
    nil
  end

  def install_gem
    exec "gem install quick_exam-#{QuickExam::VERSION}.gem"
  end

  def remove_pkg_gem
    exec "rm quick_exam-#{QuickExam::VERSION}.gem" if pkg_gem?
  rescue
    nil
  end

  def build_gem
    exec 'gem build quick_exam.gemspec'
  end

  def push_gem_to_remote
    build_gem unless pkg_gem?
    exec "gem push quick_exam-#{QuickExam::VERSION}.gem"
  end

  def remove_gem_from_remote(version)
    exec "gem yank quick_exam -v #{version} -p ruby"
  end

  def exec(cmd)
    puts "\n"
    puts '===> ' + cmd
    system cmd
  end
end

task :default => :spec
