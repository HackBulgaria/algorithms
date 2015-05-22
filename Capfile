load "deploy"

default_run_options[:pty] = true

set :scm, :none
set :scm_verbose, true

set :deploy_via, :copy

set :public_children, []

set :keep_releases, 5

task :site do
  set :application, "algorithms"

  set :user, "hack"
  set :use_sudo, false

  set :repository, "./_site"
  set :deploy_to, "/hack/#{application}"

  before "deploy:update_code" do
    run_locally "bundle exec jekyll build"
  end

  server ENV.fetch("server", "188.226.232.4"), :app, primary: true
end

namespace :deploy do
  task :finalize_update do
    # In a Rails deploy, this would create symlinks to the shared directory for
    # log, system, tmp and pids directories. We don't need those.
  end
end
