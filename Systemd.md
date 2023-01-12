# Systemd

## Common commands

``systemctl status``

List all services
``systemctl list-units -t service``

List dependencies
``systemctl list-dependencies``
A good overview of what is "on" and what is "off". 

To enable the service to start at boot
``systemctl enable name.service``

To manually start a service
``systemctl start name.service``

To restart a service
``systemctl restart name.service``

Reload config
``systemctl reload name.service``
`reload` will reload a specific service. That means that the systemd will send a SIGHUP signal to a service, and that signal will tell the service to reload its configuration files, which has nothing to do with systemd config files.

Reload custom service files
``systemctl daemon-reload``
Location of custom systemd units is "/etc/systemd/system". This command reloads the service files in that directory.

Check the configuration of a unit file
``systemctl cat sshd.service``

Edit unit file
``systemctl edit sshd.service``
By default it uses Nano. To change that to Vim.
``export SYSTEMD_EDITOR=/usr/bin/vim``
This creates a drop-in-file in "/etc/systemd/system/"
If it does not create the drop-in-file automatically, do ``systemctl daemon-reload``

To see tunables for a service do ``systemctl show httpd.service``

/user/lib/systemd/system/ is for configuration files provided by packages.
Do not edit those directly since they can be overwritten by newer packages.

/etc/tuned/ and /usr/lib/tuned/ need an explanation for it here.

Mask
To prevent certain units from starting up, use ``systemctl mask``. It links a unit to the /dev/null device, which ensures it cannot be started. For instance ``systemctl mask nginx``

``systemctl unmask`` removes the unit mask.

## Systemd Journal (journalctl)

Show all boots that have been logged. Needs to have persistent journalling.
``journalctl --list-boots``

``journalctl -xrb``
-x = Augment log lines with explanation texts from the message catalog. This will add explanatory help texts to log messages
-r = Reverse output so that the newest entries are displayed first.
-b = Show messages from a specific boot. This will add a match for "_BOOT_ID=".
The argument may be empty, in which case logs for the current boot will be shown.

### How to make the journal persistent

You could use rsyslog to make the journal persistent.

"/etc/systemd/journal.conf"
The setting "Storage=auto" ensures that persistent storage is happening automatically **after manually creating the directory** "/var/log/journal"

Then we need to restart the journal service.
``systemctl restart systemd-journal-flush.service``

### Common commands

View only messages with a priority error and higher.
``journalctl -p err``

View the last 10 lines, and adds new messages when they are added.
``journalctl -f``

Show messages for the sshd service only.
``journalctl -u sshd.service``

### See space used by Journalctl

See current settings for growth and what it's currently using.
``journalctl | grep -E 'Runtime Journal|System Journal'``


## Systemd Timers (Scheduling)

When using systemd timers, the timer should be started, and **not** the service unit.

``systemctl list-units -t timer``
``systemctl list-unit-files dnf-makecache*``
``systemctl status dnf-makecache.timer``
Checkout the "Trigger and Triggers".

To schedule and activate a timer you use the "OnCalendar" option.

``OnCalendar=*:00/20`` runs every 20 minutes.

You can use "OnUnitActiveSec" to start the unit at a specific time after the unit was last activated.

You can use "OnBootSec" or "OnStartupSec" to start the unit a specific time after booting.

## Working with Tuned

Install tuned. ``dnf install tuned``

To see available commands, type this in and press double tab. ``tuned-adm`` 

To see available profiles. ``tune-adm list``

Config files for Tuned are located in "/usr/lib/tuned/".








