# encoding: utf-8

task default: [:quality]
task quality: [:rubocop, :reek]
task travis: [:quality]

Dir.glob('tasks/*.rake').each { |each| import each }
