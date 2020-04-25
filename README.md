# GerNOX PDKSync Config

## Usage

1. To use pdksync, clone the GitHub repo or install it as a gem. Set up the environment by exporting a GitHub token:

   ```shell
   export GITHUB_TOKEN=<access_token>
   ```

2. Before the script will run, you need to install the gems:
   ```shell
   bundle install --path .bundle/gems/
   ```
   
3. Once this is complete, call the built-in rake task to run the module:
   ```shell
   bundle exec rake pdksync
   ```

## Available Rake Tasks

The following rake tasks are available with pdksync:
- `pdksync:show_config` Display the current configuration of pdksync
- `git:clone_managed_modules` Clone managed modules.
- `git:create_commit[:branch_name, :commit_message]` Stage commits for modules, branchname and commit message eg rake 'git:create_commit[flippity, commit messagez]'.
- `git:push` Push staged commits eg rake 'git:push'.
- `git:create_pr[:pr_title, :label]` Create PR for modules. Label is optional eg rake 'git:create_pr[pr title goes here, optional label right here]'.
- `git:clean[:branch_name]` Clean up origin branches, (branches must include pdksync in their name) eg rake 'git:clean[pdksync_origin_branch]'.
- `pdksync:pdk_convert` Runs PDK convert against modules.
- `pdksync:pdk_validate` Runs PDK validate against modules.
- `pdksync[:additional_title]` Run full pdksync process, clone repository, pdk update, create pr. Additional information can be added to the title, which will be appended before the reference section.
  - `rake pdksync` PR title outputs as `pdksync - pdksync_heads/master-0-gabccfb1`
  - `rake 'pdksync[MODULES-8231]'` PR title outputs as `pdksync - MODULES-8231 - pdksync_heads/master-0-gabccfb1`
- `pdksync:run_a_command[:command, :option]` Run a command against modules eg rake 'pdksync:run_a_command[complex command here -f -gx, 'background']'. :option is an optional parameter which states to run command in backgroud.
- `pdksync:gem_file_update[[:gem_to_test, :gem_line, :gem_sha_finder, :gem_sha_replacer, :gem_version_finder, :gem_version_replacer, :gem_branch_finder, :gem_branch_replacer]]` Run gem_file_update against modules
  - eg rake to update gem line `pdksync:gem_file_update['puppet_litmus', "gem 'puppet_litmus'\, git: 'https://github.com/test/puppet_litmus.git'\, branch: 'testbranch'"]'`
  - eg rake to update sha `pdksync:gem_file_update['puppet_litmus', '', '20ee04ba1234e9e83eb2ffb5056e23d641c7a018', '20ee04ba1234e9e83eb2ffb5056e23d641c7a31']`
  - eg rake to update version`pdksync:gem_file_update['puppet_litmus', '', '', '', "= 0.9.0", "<= 0.10.0", '', '']`
  - eg rake to update branch `pdksync:gem_file_update['puppet_litmus', '', '', '', '', '', 'testbranch', 'testbranches']`
- `rake 'gem_testing[:additional_title, :gem_to_test, :gem_line, :gem_sha_finder, :gem_sha_replacer, :gem_version_finder, :gem_version_replacer, :gem_branch_finder, :gem_branch_replacer]'` Run complete Gem file testing (cloning, gemfileupdate, create commit, create PR)PR title outputs as `pdksync_gemtesting - MODULES-8231 - pdksync_heads/master-0-gabccfb1`
  - eg rake to perform gem file testing `gem_testing['MODULES-testing', 'puppet_litmus', '', '20ee04ba1234e9e83eb2ffb5056e23d641c7a018', 'testsha']`
- `pdksync:run_tests_locally[:provision_type, :puppet_collection]` Run litmus modules locally
  - eg rake 'pdksync:run_tests_locally["default"]'
- `pdksync:fetch_test_results_locally[]` Fetch litmus modules local run results
  - eg rake 'pdksync:fetch_test_results_locally[]'
- `pdksync:run_tests_jenkins[:jenkins_server_url, :github_branch, :test_framework, :github_user]` Run traditional modules on jenkins. For now this rake task works just for test_framework: jenkins.
  - eg rake 'pdksync:run_tests_jenkins[test_branch, '', test_user]'
- `pdksync:test_results_jenkins[]` Fetch traditional modules jenkins run results
  - eg rake 'pdksync:test_results_jenkins[jenkins_server_url]'
- `git:clone_gem[:gem_name]` Clone gem.
- `pdksync:multi_gem_testing[:gem_name, :version_file, :build_gem, :gem_path, :gemfury_username]` Build and Push new gems built to the gemfury account for testing eg rake 'pdksync:multi_gem_testing[]'
- `pdksync:multigem_file_update[:gem_name, :gemfury_username]` Update Gemfile of the modules with the new gem should be pushed to Gemfury.'

