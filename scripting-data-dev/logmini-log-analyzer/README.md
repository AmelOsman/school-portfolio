# logmini: Bash Log Analyzer

**Course:** Scripting Language (IT 3038C) · **Term:** Fall 2025 · **Type:** Individual final project

🔗 **[View the code on GitHub →](https://github.com/AmelOsman/logmini)**

## Overview
`logmini` is a command-line tool I wrote in Bash for quick log triage on Linux systems. It summarizes one or more log files by severity level, or pulls out specific events with a regular expression. It's the kind of small automation a SOC analyst or sysadmin uses to spot problems fast, like a burst of failed logins or a sudden spike in errors.

## Tools & Technologies
Bash · `getopts` · `grep` (POSIX extended regex) · `awk` · Linux

## Features
- **Severity summary:** counts CRITICAL, FATAL, ERROR, WARN, NOTICE, INFO, and DEBUG entries, case-insensitive
- **Event mode:** prints only the lines matching a regex
- **Multiple log files** in a single run
- **Save to file** for reports
- **Defensive scripting:** strict mode, input validation, and clear error and help messages

## Example
Investigating a suspicious IP address across a log:
```console
$ ./logmini.sh -f sample.log -e -p '203\.0\.113\.45'
2025-10-01 08:02:14 WARNING sshd[1188]: Failed password for invalid user admin from 203.0.113.45
2025-10-01 08:02:16 WARNING sshd[1188]: Failed password for invalid user admin from 203.0.113.45
2025-10-01 08:02:19 ERROR sshd[1188]: Too many authentication failures for admin from 203.0.113.45
```

Summarizing the whole log by severity:
```console
$ ./logmini.sh -f sample.log
CRITICAL 1
FATAL    0
ERROR    2
WARN     2
NOTICE   1
INFO     2
DEBUG    1
TOTAL    9
```

## What I Learned
- Parsing command-line options with `getopts` and validating user input
- Building text-processing pipelines with `grep` and `awk`
- Writing safer scripts with `set -euo pipefail`, and handling the edge cases it exposes
- How log analysis supports security monitoring and incident triage
