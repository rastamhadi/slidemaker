require 'yaml'
require 'erb'
require 'pathname'
require 'rake/clean'

PROJECT_NAME = Pathname.new(Dir.pwd).basename.freeze
USERNAME = `whoami`.strip.freeze

SLIDEMAKER_PATH = Pathname.new('../../slidemaker').freeze

task default: :work

desc 'Launch the project in Google Chrome, Sublime Text and Guard'
task work: [:sublime, :chrome, :guard]

namespace :host do
  desc 'Host the slides locally and print the URL'
  task url: :host do
    puts url
  end
end

desc 'Host the slides locally'
task host: "/Users/#{USERNAME}/Sites/#{PROJECT_NAME}"

desc 'Launch the slides in Google Chrome'
task chrome: 'slides/index.html' do |t|
  sh "open #{t.source}"
end

desc 'Guard the project'
task guard: :init do
  sh 'rbenv exec bundle exec guard'
end

desc 'Launch the project in Sublime Text'
task sublime: :init do
  sh 'sublime .'
end

desc 'Generate a new reveal-ck project'
task init: ['Gemfile.lock', 'Guardfile', 'slides/index.html']

SYM_LINK_PATH = "/Users/#{USERNAME}/Sites/#{PROJECT_NAME}".freeze
file SYM_LINK_PATH => 'slides/index.html' do |t|
  sh "ln -s #{Pathname.new(t.source).parent.realpath} #{t.name}"
end
CLOBBER.include(SYM_LINK_PATH)

file 'slides/index.html' => 'slides.md' do
  sh 'reveal-ck generate'
end
CLOBBER.include('slides')

file 'slides.md' => [SLIDEMAKER_PATH.join('erb', 'slides.md.erb'), 'config.yml'] do |t|
  title = YAML.load_file(t.sources.last)['title']
  render_erb(t.source, t.name, title)
end
CLOBBER.include('slides.md')

file 'config.yml' => SLIDEMAKER_PATH.join('erb', 'config.yml.erb') do |t|
  puts 'What is the title of your slides?'
  title = $stdin.gets.chomp
  render_erb(t.source, t.name, title)
end
CLOBBER.include('config.yml')

file 'Gemfile.lock' => ['Gemfile', '.ruby-version'] do
  sh 'rbenv exec bundle install'
end
CLOBBER.include('Gemfile.lock')

Rake::FileList.new(SLIDEMAKER_PATH.join('templates', '*')).each do |template|
  file template.pathmap('%f') => template do |t|
    cp t.source, t.name
  end
  CLOBBER.include(template.pathmap('%f'))
end

file '.ruby-version' do
  sh "rbenv versions | tail -n1 | awk '{$1=$1};1' > .ruby-version"
end
CLOBBER.include('.ruby-version')

def url
  "http://#{`ipconfig getifaddr en0`.strip}/~#{USERNAME}/#{PROJECT_NAME}"
end

def render_erb(erb_path, out_path, title)
  erb = ERB.new(File.read(erb_path)).result(binding)
  open(out_path, "w+") { |f| f.write(erb) }
end
