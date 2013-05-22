# sshame

I wrote `sshame` to collect IP addresses and information about bad
authentication attempts on my servers.

## Requirements

`sshame` needs [Ruby](http://ruby-lang.org/), and an `sshd` authentication
log (probably `auth.log`).

## Installation

The `sshame` script in this directory should be put somewhere in your
executable path.

## Simple Usage

`sshame` expects to receive a log file from `stdin`, or for a path to
be specified by the `-f` option. For example:

```bash
$ cat auth.log | sshame
221.176.53.74
129.194.160.23
61.142.106.34

$ sshame -f auth.log
221.176.53.74
129.194.160.23
61.142.106.34
```

## Additional Options

To display a count of failed attempts for each IP address, use the `-c`
option. For example:

```bash
$ sshame -f auth.log -c
221.176.53.74   32
129.194.160.23	72
61.142.106.34   3
```

_Note: the output is tab delimited for ease of parsing._

To change the threshold for how many failed attempts per IP address,
use the `-t` option. For example:

```bash
$ sshame -f auth.log -t 70
129.194.160.23	72
```

For a comma delimited list of the usernames associated with the failed attempts, use the
`-l` option. For example:

```bash
$ sshame -f auth.log -l
61.142.106.34   operator,ruser,tose
```

And of course all of these options can be combined as you see fit:

```bash
$ sshame -f auth.log -l -c -t 50
129.194.160.23  72        a,seinfeld,contest,princess,maggie,...
```