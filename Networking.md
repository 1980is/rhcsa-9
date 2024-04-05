# Networking

## Notes

Do not use ifconfig anymore. It's been deprecated for over 20 years now.
Ifconfig does not support secondary ip addresses for example.

## See information for your NIC

### Display IP addresses
``ip ad`` or ``nmcli``

### Display route/gateway information
``ip -4 route``
``ip -6 route``

Legacy command to see route information.
``netstat -rn`` or ``route -n``

### Display ARP table
``arp -a``

### Display the ARP default timeout
``cat cat /proc/sys/net/ipv4/neigh/default/gc_stale_time``

## Change settings for your NIC

### Assign IP address

You can use the "graphical" ``nmtui`` tool to configure your network connection. If you use ``nmtui``, remember to **set the subnet mask** when you enter the ip address. Using ``nmtui`` for the exam is better, it will save time.

![nmtui](pictures/nmtui.png)

Another way is to use the ``nmcli`` tool. Remember to swap out the name for the correct name you see when you execute ``nmcli connection show``
 ``nmcli connection edit enp1s0``

Now you are in the nmcli interface. Type ``print`` to see detailed information for the connection named "enp1s0". To see the name of all your connection, ``nmcli connection show`` and ``nmcli device show``

Find the connection name, ``nmcli connection show``
Make sure that the **bash-completion package** is installed when working with nmcli.

Assign the IP address to the correct connection name.
``nmcli connection modify enp0s3 ipv4.addresses 192.168.1.21/24``

ip is an excellent command for troubleshooting but using the ip command only changes runtime environment, **it does not change anything in the configuration files.**

Here are a few nmcli examples:

``nmcli device status`` \
``nmcli connection show -active`` \
If the connection is unmanaged or not connecting, try this command. \
``sudo nmcli connection mod <connection-name> connection.autoconnect yes``

**Activate Changes** \
``nmcli connection reload`` \
This only makes the NM aware of the changes. \
You have to take the connection down and then up (``nmcli con down NAME; nmcli con up NAME``) or most changes can be applied directly with ``nmcli dev reapply NAME``

### Change the gateway

``nmcli connection modify enp0s3 ipv4.gateway 192.168.1.254``

### Use static instead of DHCP

``nmcli connection modify enp0s3 ipv4.method static``

### Disabling and enabling an interface
``ip link set ens33 down``
``ip link set ens33 up``

### Changing the MTU for e.g., iSCSI
``nmcli con mod ensp92 802-3-ethernet.mtu 9000``

## Firewall (netfilter/nftables)

On the exam it's better to restart services than to reload them.

The netfilter framework in the Linux kernel manages firewall operations, and it forwards specific operations to kernel modules.
- Packet filtering
- Network address translation
- Port forwarding

### Firewalld

Firewalld is a good interface to create and manage a simple firewall but the framework behind it is the Netfilter (nftables) firewall. 

To see config files for services, check out.
"/usr/lib/firewalld/"

### General commands

``firewall-cmd --list-all``

``firewall-cmd --get-services``

``firewall-cmd --add-service squid --permanent`` \
Remember to use the permanent switch, otherwise the rule is written only to the runtime and is lost if you restart firewalld or the server!

``firewall-cmd --reload``

### Zones

A zone is a default configuration to which network cards can be assigned to apply specific settings. 

### Service

You only need to know the service part for the RHCSA exam!

### Ports

Optional elements to allow access to specific ports.

## Network Sockets

Use ``ss`` to show socket information. This will show all connections.

``ss -tu`` shows connected TCP and UDP sockets.

``ss -tua`` shows connected TCP and UDP sockets + sockets in a listening state.

``ss -tulpn`` Shows TCP and UDP sockets in a listening state, it also adds process names or PID to the output. 



## Debug

- Use ``nm-connection-editor`` if you have issues with certs for you network cards.
- Make sure your subnet mask is correct.
- Ping your gateway to see if you can reach the router.
- DNS not working, check "/etc/resolv.conf" to make sure it's correct.
