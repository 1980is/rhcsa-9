# Firewall

On the exam it's better to restart services than to reload them.

## Firewalld

To see config files for services, check out.
"/usr/lib/firewalld/"

### General commands

``firewall-cmd --list-all``

``firewall-cmd --get-services``

``firewall-cmd --add-service squid --permanent``

``firewall-cmd --reload``
