# Managing processes

---

## General notes

Use cgroups instead of nice and renice to manage processes.

To list, read, and set kernel tunables.
``sysctl -a``

To make system tuning easier, use ``tuned``
``tuned`` is a systemd service that works with different profiles.
``tuned-adm list`` shows current profiles.


---