# Random Notes

---

## Sudo

Extend the auth token for sudo. The default is 5 minutes. Put this line into "/etc/sudoers" file. 60, equals 60 minutes.

``Defaults timestamp_type=global,timestamp_timeout=60``

