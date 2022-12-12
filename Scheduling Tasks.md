# Scheduling Tasks

For the exam, don't study and learn about crond. Study and learn about crond for real world legacy systems that you work on everyday. **Systemd timers** is what is primarily used on RHEL 9 and that's reflected on the exam.

``systemctl list-units -t timer``

**Logrotate example.**

"/usr/lib/systemd/system/"
``ls logro*``
You will see "logrotate.timer"

``systemctl cat logrotate.timer``

``systemctl status logrotate.service``
You will see a line.
"TriggeredBy: ● logrotate.timer"

