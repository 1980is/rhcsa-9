# Configure time service clients

``hwclock`` sets the hardware time.
If the hardware clock is not correct but the system time is you can sync the hardware time to the 
system time with ``hwclock --systohc``

Use ``date`` so show current date and time.

Use ``timedatectl`` to manage time and time zone configuration.

``timedatectl status`` show all time properties in use.
``timedatectl set-time`` \
``timedatectl set-timezone`` \
``timedatectl set-ntp`` enables or disables NTP sync.

An NTP service must be configured. The default for RHEL is Chrony.
If your server is running **systemd-timesyncd.service** you must disable that service before enabling Chrony.

## Chronyd
Chronyd is the default RHEL 9 NTP service.
Use "/etc/chrony.conf" to change sync parameters.

Use iburst to permit fast synchronization.

After changing the conf file restart the chronyd service.

``chronyc sources`` to see the servers you are synchronizing with.









