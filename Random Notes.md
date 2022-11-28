# Random Notes

## Bash completion

Install bash completion on the exam if it's missing.
``sudo dnf install bash-completion``

## Sudo

Extend the auth token for sudo. The default is 5 minutes. Put this line into "/etc/sudoers" file. 60, equals 60 minutes.

``Defaults timestamp_type=global,timestamp_timeout=60``

