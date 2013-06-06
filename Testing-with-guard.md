When running tests via guard, cleaning up after test dependencies (eg. starting a Ruby server) was not very straightforward. Combined with Pry where Ctrl+C gets remapped to Ctrl+D, this was getting fairly unmanageable. Here's my bash wrapper which ensures that a processes gets started and stopped correctly:

```bash
#!/usr/bin/env bash
# saved as bin/guard
set -e

api_server_pid_file="tmp/api_test_server.pid"

stop_api_server() {
  if [[ -e $api_server_pid_file ]]
  then
    kill -INT "$(cat $api_server_pid_file)"
  fi
}

graceful_stop() {
  stop_api_server
  exit 0
}

# traps Ctrl+D (EOF)
trap graceful_stop 0

bundle exec ruby test/support/api_server.rb
bundle exec guard
```

The only gotcha is Ctrl+C which will stop the server in my example, but the test runner ensures that it's available for any tests that require it.