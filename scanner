#!/bin/bash

# +----------------------------------------------------------------------------+
# | Name: scanner                                                              |
# |                                                                            |
# | Purpose: Port scanner (TCP) implemented in bash                            |
# |                                                                            |
# | Date Created: 2012/09/16                                                   |
# | Date Modified: 2013/11/08                                                  |
# |                                                                            |
# | Usage: source this file first: . scanner                                   |
# |        scan <host> <port, ports, port-range>                               |
# |                                                                            |
# | Example: scan google.com 80                                                |
# |          scan google.com 78-82                                             |
# |          scan google.com 25,80,443                                         |
# +----------------------------------------------------------------------------+

# +----------------------------------------------------------------------------+
# | function alarm                                                             |
# |                                                                            |
# | Description: waits $1 amount of seconds before killing $2                  |
# |                                                                            |
# | Arguments:                                                                 |
# |   $1: number of seconds                                                    |
# |   $2: command to execute in bash shell                                     |
# |                                                                            |
# | Returns:                                                                   |
# |   0 if command had to be killed (if port is open, process will be killed)  |
# |   not a 0 if command wasn't killed (if port is closed, process dies)       |
# +----------------------------------------------------------------------------+
alarm() {
  local timeout=$1; shift;
  # execute command, store PID
  bash -c "$@" &
  local pid=$!
  # sleep for $timeout seconds, then attempt to kill PID
  {
    sleep "$timeout"
    kill $pid 2> /dev/null
  } &
  wait $pid 2> /dev/null 
  return $?
}

# +----------------------------------------------------------------------------+
# | function scan                                                              |
# |                                                                            |
# | Description: attempts to write to /dev/tcp/$1/$2; if write is successful,  |
# |   port is open.                                                            |
# |                                                                            |
# | Arguments:                                                                 |
# |   $1: host or IP                                                           |
# |   $2: port(s) or port range                                                |
# |                                                                            |
# | Returns:                                                                   |
# |   Nothing                                                                  |
# +----------------------------------------------------------------------------+
scan() {
  if [[ -z $1 || -z $2 ]]; then
    echo "Usage: scan <host> <port, ports, or port-range>"
    echo "Example: scan google.com 79-81"
    return
  fi

  local host=$1
  local ports=()
  # store user-provided ports in array
  case $2 in
    *-*)
      IFS=- read start end <<< "$2"
      for ((port=start; port <= end; port++)); do
        ports+=($port)
      done
      ;;
    *,*)
      IFS=, read -ra ports <<< "$2"
      ;;
    *)
      ports+=($2)
      ;;
  esac

  # attempt to write to each port, print open if successful, closed if not
  for port in "${ports[@]}"; do
    alarm 1 "echo >/dev/tcp/$host/$port" &&
      echo "$port/tcp open" ||
      echo "$port/tcp closed"
  done
}
