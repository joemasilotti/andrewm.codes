require "bridgetown"

Bridgetown.load_tasks

# Run rake without specifying any command to execute a deploy build by default.
task default: :deploy

#
# Standard set of tasks, which you can customize if you wish:
#
desc "Build the Bridgetown site for deployment"
task deploy: [:clean, "frontend:build"] do
  Bridgetown::Commands::Build.start
end

desc "Build the site in a test environment"
task :test do
  ENV["BRIDGETOWN_ENV"] = "test"
  Bridgetown::Commands::Build.start
end

desc "Runs the clean command"
task :clean do
  Bridgetown::Commands::Clean.start
end

namespace :frontend do
  desc "Build the frontend with esbuild for deployment"
  task :build do
    sh "yarn run esbuild"
  end

  desc "Watch the frontend with esbuild during development"
  task :dev do
    sh "yarn run esbuild-dev"
  rescue Interrupt
  end
end

desc "Runs the format commands"
task format: ["format:standard", "format:prettier"]

namespace :format do
  desc "Format with Standard"
  task :standard do
    sh "bin/standardrb"
  end

  desc "Format with Prettier"
  task :prettier do
    sh "yarn prettier --write ."
  rescue Interrupt
  end
end

desc "Runs the update commands"
task update: ["update:cssdb", "update:yarn"]

namespace :update do
  desc "Update browserlists db"
  task :cssdb do
    sh "npx browserslist@latest --update-db"
  end

  desc "Update yarn dependencies"
  task :yarn do
    sh "yarn upgrade-interactive --latest && yarn upgrade"
  rescue Interrupt
  end
end

#
# Add your own Rake tasks here! You can use `environment` as a prerequisite
# in order to write automations or other commands requiring a loaded site.
#
# task :my_task => :environment do
#   puts site.root_dir
#   automation do
#     say_status :rake, "I'm a Rake tast =) #{site.config.url}"
#   end
# end