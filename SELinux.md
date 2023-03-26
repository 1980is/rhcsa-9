# SELinux

Selinux state is either enabled or disabled. You must reboot to switch between the two.
Enabled has two modes, permissive or enforcing.

If you want to temporarily disable SELinux to debug or analyze something you should
change the SELinux state while booting by using a kernel parameter.

- enforcing=0 will start SELinux in permissive mode. 
- enforcing=1 will start SELinux in enforcing mode.
- selinux=0 will disable SELinux.

``getenforce`` to see the status of SELinux.

``setenforce`` to switch between modes, permissive or enforcing. This is temporary, it will go back
to whatever is defined in "/etc/selinux/config" after the server is rebooted.

``ps Zaux``

## Context and Context types

### Context

Remember to look at `` man semanage-fcontext`` during the exam. At the bottom you have examples you can use.

When files are created in a directory, they typically inherit the context of the parent directory and most services don't need additional SELinux configuration if default settings are used.

When files are copied, they typically inherit the context of the parent directory. If it's not relabeled correctly you can use ``restorecon -Rv /mydirectory`` 

Use ``semanage fcontext`` to set the file context label. This will write the context to the SELinux Policy, but **it is not written yet to the filesystem**.
A second step is necessary to write it to the filesystem by using ``restorecon``

Instead of using ``restorecon`` you can use ``touch /.autorelabel`` to relabel all files to the context that is specified in the policy. That should be our last option, it happens while rebooting.
So ``restorecon`` is preferred.


Use ``semanage fcontext -a`` to set a new context label.

Use ``semanage fcontext -m`` to modify an existing context label.

**Important for the exam!** See ``man semanage-fcontect`` for documentation.

If you apply non-default configuration, check the default configuration context setting but if that's not available install the man pages with  ``dnf install selinux-policy-doc`` and then ``man -k _selinux | grep http`` as an example.

Do **NOT** use ``chcon`` as the changes it makes may be overwritten.

Use ``semanage fcontext -I -C`` to show only settings that have changed in the current policy.

### Context Types

In most configurations, only context type matters, so you can safely ignore user and role for RHCSA. Every object is labeled with a context label.

- user: user specific context
- role: role specific context
- type: flags which type of operation is allowed on this object


Many commands support the -Z option to see the context for files.
``ls -Z /etc/``

Context types are used in the rules in the policy to define which source object has access to which target object.

### Booleans

A boolean is an easy-to-use configuration switch to enable or disable specific parts of the SELinux policy.

For an overview of all booleans, use ``semanage boolean -I`` or ``getsebool -a``.

To see all booleans that have a non-default setting ``semanage boolean -l -C`` 

An example to learn from. ``getsebool -a | grep ftp``

### Networking

Network ports are also provided with an SELinux context label. The SELinux policy is configured to allow default port access. For any non-default port access, use ``semanage-port`` to apply the right label to the port.

Use the examples section in man ``semanage-port`` for examples.

### Debug

Check to see if SEAlert is installed. ``dnf provides */sealert``

``journalctl | grep sealert``
