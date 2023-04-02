# Reset Root Password

Things have changed in RHEL 9. rd.break does not work anymore.
These are the steps that need to be taken.

1. Find the line that loads the Linux kernel and add ``init=/bin/bash`` to the end of the line.
2. ``mount -o remount,rw /`` This is necessary because it's mounted as read-only.
3. ``passwd root``
4. ``touch /.autorelabel``
5. ``exec /usr/lib/systemd/systemd/`` To reboot the machine or ``/sbin/reboot -f``