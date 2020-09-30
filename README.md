# tmp-rubocop-json-formatter-issue

This repository is just for reproducing [this](https://github.com/rubocop-hq/rubocop/issues/8718) issue.

Here's my environment.

```console
$ bundle exec rubocop -V
0.92.0 (using Parser 2.7.1.5, rubocop-ast 0.7.1, running on ruby 2.7.1 x86_64-linux)
```

I don't get any errors with the following command (without `--format=json`):

```console
$ bundle exec rubocop --cache=false a.rb
Inspecting 1 file
W

Offenses:

a.rb:1:1: W: Lint/EmptyFile: Empty file detected.

1 file inspected, 1 offense detected
```

However, with `--format=json`, I can get this error.

```console
$ bundle exec rubocop --cache=false --format=json a.rb
{"metadata":{"rubocop_version":"0.91.0","ruby_engine":"ruby","ruby_version":"2.7.1","ruby_patchlevel":"83","ruby_platform":"x86_64-linux"},"files":[],"summary":{"offense_count":0,"target_file_count":1,"inspected_file_count":0}}undefined method `last_line' for #<RuboCop::Cop::Offense::PseudoSourceRange:0x0000560e6a864c40>
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/rubocop-0.91.0/lib/rubocop/cop/offense.rb:175:in `last_line'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/rubocop-0.91.0/lib/rubocop/formatter/json_formatter.rb:70:in `hash_for_location'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/rubocop-0.91.0/lib/rubocop/formatter/json_formatter.rb:61:in `hash_for_offense'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/rubocop-0.91.0/lib/rubocop/formatter/json_formatter.rb:50:in `block in hash_for_file'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/rubocop-0.91.0/lib/rubocop/formatter/json_formatter.rb:50:in `map'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/rubocop-0.91.0/lib/rubocop/formatter/json_formatter.rb:50:in `hash_for_file'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/rubocop-0.91.0/lib/rubocop/formatter/json_formatter.rb:28:in `file_finished'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/rubocop-0.91.0/lib/rubocop/formatter/formatter_set.rb:49:in `block in file_finished'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/rubocop-0.91.0/lib/rubocop/formatter/formatter_set.rb:49:in `each'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/rubocop-0.91.0/lib/rubocop/formatter/formatter_set.rb:49:in `file_finished'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/rubocop-0.91.0/lib/rubocop/runner.rb:214:in `file_finished'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/rubocop-0.91.0/lib/rubocop/runner.rb:123:in `process_file'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/rubocop-0.91.0/lib/rubocop/runner.rb:97:in `block in each_inspected_file'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/rubocop-0.91.0/lib/rubocop/runner.rb:96:in `each'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/rubocop-0.91.0/lib/rubocop/runner.rb:96:in `reduce'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/rubocop-0.91.0/lib/rubocop/runner.rb:96:in `each_inspected_file'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/rubocop-0.91.0/lib/rubocop/runner.rb:82:in `inspect_files'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/rubocop-0.91.0/lib/rubocop/runner.rb:43:in `run'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/rubocop-0.91.0/lib/rubocop/cli/command/execute_runner.rb:25:in `execute_runner'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/rubocop-0.91.0/lib/rubocop/cli/command/execute_runner.rb:17:in `run'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/rubocop-0.91.0/lib/rubocop/cli/command.rb:11:in `run'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/rubocop-0.91.0/lib/rubocop/cli/environment.rb:18:in `run'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/rubocop-0.91.0/lib/rubocop/cli.rb:65:in `run_command'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/rubocop-0.91.0/lib/rubocop/cli.rb:72:in `execute_runners'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/rubocop-0.91.0/lib/rubocop/cli.rb:41:in `run'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/rubocop-0.91.0/exe/rubocop:13:in `block in <top (required)>'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/2.7.0/benchmark.rb:308:in `realtime'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/rubocop-0.91.0/exe/rubocop:12:in `<top (required)>'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/bin/rubocop:23:in `load'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/bin/rubocop:23:in `<top (required)>'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/bundler-2.1.4/lib/bundler/cli/exec.rb:63:in `load'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/bundler-2.1.4/lib/bundler/cli/exec.rb:63:in `kernel_load'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/bundler-2.1.4/lib/bundler/cli/exec.rb:28:in `run'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/bundler-2.1.4/lib/bundler/cli.rb:476:in `exec'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/bundler-2.1.4/lib/bundler/vendor/thor/lib/thor/command.rb:27:in `run'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/bundler-2.1.4/lib/bundler/vendor/thor/lib/thor/invocation.rb:127:in `invoke_command'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/bundler-2.1.4/lib/bundler/vendor/thor/lib/thor.rb:399:in `dispatch'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/bundler-2.1.4/lib/bundler/cli.rb:30:in `dispatch'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/bundler-2.1.4/lib/bundler/vendor/thor/lib/thor/base.rb:476:in `start'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/bundler-2.1.4/lib/bundler/cli.rb:24:in `start'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/bundler-2.1.4/exe/bundle:46:in `block in <top (required)>'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/bundler-2.1.4/lib/bundler/friendly_errors.rb:123:in `with_friendly_errors'
/home/kamei/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/bundler-2.1.4/exe/bundle:34:in `<top (required)>'
/home/kamei/.rbenv/versions/2.7.1/bin/bundle:23:in `load'
/home/kamei/.rbenv/versions/2.7.1/bin/bundle:23:in `<main>'
```
