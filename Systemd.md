# Systemd

## Common commands

``systemctl status``

**List all services**
``systemctl list-units -t service``

**List dependencies**
``systemctl list-dependencies``
A good overview of what is "on" and what is "off". 

**To enable the service to start at boot**
``systemctl enable name.service``

**To manually start a service**
``systemctl start name.service``

**To restart a service**
``systemctl restart name.service``

**Reload config**
``systemctl reload name.service``
`reload` will reload a specific service. That means that the systemd will send a SIGHUP signal to a service, and that signal will tell the service to reload its configuration files, which has nothing to do with systemd config files.

**Reload custom service files**
``systemctl daemon-reload``
Location of custom systemd units is "/etc/systemd/system". This command reloads the service files in that directory.

**Check the configuration of a unit file**
``systemctl cat sshd.service``

**Edit unit file**
``systemctl edit sshd.service``
By default it uses Nano. To change that to Vim.
``export SYSTEMD_EDITOR=/usr/bin/vim``
This creates a drop in file in "/etc/systemd/system/"

/user/lib/systemd/system/ is for configuration files provided by packages.

/etc/tuned/ and /usr/lib/tuned/ need an explanation for it here.

## Systemd Journal

``journalctl -xrb``

**How to make the journal persistent**

You could use rsyslog to make the journal persistent.

"/etc/systemd/journal.conf"
The setting "Storage=auto" ensures that persistent storage is happening automatically **after manually creating the directory** "/var/log/journal"

Then we need to restart the journal service.
``systemctl restart systemd-journal-flush.service``


