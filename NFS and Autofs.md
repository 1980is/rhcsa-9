# NFS and Autofs (Automount)

## NFS

NFS is not a part of the RHCSA exam. It's just something we need to set up to work on autofs. I had two machines, the nfsserver and the client machine. On the nfsserver, do the following.

Install NFS server.
``dnf install nfs-utils``

Create the directory that you want to export. 
``mkdir /nfsdata``

Put it into the exports file. ``vim /etc/exports`` \
This is just an example, it's insecure, don't use it. ``/nfsdata *(rw,no_root_squash)``

Enable and start the NFS server in one command.
``systemctl enable --now nfs-server``

To quickly open up the firewall to allow NFS. It adds the nfs, mountd and rpc-bind services to the firewall services.

``for i in nfs mountd rpc-bind; do firewall-cmd --add-service $i --permanent; done``

``firewall-cmd --reload``

``firewall-cmd --list-all``

## Autofs

On the exam, check **"/etc/auto.misc"** for nice syntax examples that can help if you're stuck!
You won't see auto.misc until you have installed the autofs package.

Now on the client that will be using autofs, do the following.

First make sure you can see the exports on from the NFS Server.

``showmount -e nfsservername``

Automount is common for home directories. An NFS server is providing access to home directories, and the home directory is automounted when the user logs in.

Install autofs.

``dnf install autofs``

In "/etc/auto.master" you'll identify the directory that automount should manage, and the file that is used for additional mount information.

- "/nfsdata" and "/etc/auto.nfsdata"
- "/nfsdata" is the mounting point and the second line "/etc/auto.nfsdata" is a file you create that gives the necessary parameters to mount it.
- In "/etc/auto.nfsdata" you'll identify the subdirectory on which to mount, and what to mount.
- files -rw nfsservername:/nfsdata

Files is a subdirectory under /nfsdata that is created when you cd into it.

For nfsserver, put the ip or the DNS name of the server you want to automount from.

Enable and start the autofs service.
``systemctl enable --now autofs``

This will automatically create the folders necessary under the root "/" folder. In this example it creates the ''/misc" and "/nfsdata" folders. If you cd /nfsdata, it should be empty. If you ``cd`` into files, even though /nfsdata is empty you will cd into the /nfsdata directory on the nfsserver.

### Home directories

To support different directory names in one automount line, wildcards are used.

Put the following line in "/etc/auto.master".
/home/ldap    /etc/auto.ldap
This auto mounts all subdirectories under /ldap.

Let's create the file "/etc/auto.ldap".

``vim /etc/auto.ldap``

Insert the line.
``*    -rw  localhost:/home/ldap/&``

Let's say you have multiple home directories under "/home/ldap/1", "/home/ldap/2", etc. The ampersand at the end replaces whatever comes after /ldap/.

When that is done.
``systemctl restart autofs``



