# Networking

## Notes

Do not use ifconfig anymore. It's been deprecated for over 20 years now. Ifconfig does not support secondary ip addresses for example.

---

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

---

## Change settings for your NIC

### Assign IP address

You can use the graphical ``nmtui`` tool to configure your network connection. If you use ``nmtui``, remember to **set the subnet mask** when you enter the ip address. Using ``nmtui`` for the exam is better, it will save time.

![nmtui](pictures/nmtui.png)

Another way is to use the ``nmcli`` tool. Rememer to swap out the name for the correct name you see when you execute ``nmcli connection show``
 ``nmcli connection edit enp1s0``

Now you are in the nmcli interface. Type ``print`` to see detailed information for the connection named "enp1s0". To see the name of all your connection, ``nmcli connection show`` and ``nmcli device show``

Find the connection name, ``nmcli connection show``
Make sure that the **bash-completion package** is installed when working with nmcli.

Assign the IP address to the correct connection name.
``nmcli connection modify enp0s3 ipv4.addresses 192.168.1.21/24``

ip is an excellent command for troubleshooting but using the ip command only changes runtime environment, **it does not change anything in the configuration files.**

## Change the gateway

``nmcli connection modify enp0s3 ipv4.gateway 192.168.1.254``

## Use static instead of DHCP

``nmcli connection modify enp0s3 ipv4.method static``

### Disabling and enabling an interface
``ip link set ens33 down``
``ip link set ens33 up``

### Changing the MTU for e.g., iSCSI
- ``nmcli con mod ensp92 802-3-ethernet.mtu 9000``

---

NMCLI and NMTUI 

-   man nmcli-examples 
    
-   nmtui is a graphical editor for network manager config files. 
    
    -   These files are located in /etc/sysconfig/network-scripts/name-of-network-card 

DNS 

-   dnf install bind-utils 
    

-   nmcli device show enp0s13f0u2u3  
    

Ubuntu Find DNS servers 

-   cat /etc/netplan/00-installer-config.yaml 
    
-   systemd-resolve --status | grep Current 
    

Ubuntu Breyta DNS servers 

-   Tímabundin breyting. 
    
    -   Vim /run/systemd/resolve/stub-resolv.conf 
        
-   Langtíma breyting. 
    
    -   vim /etc/netplan/*.yaml 
        

DEBUG ON DNS 

-   btw ef þú hefur áhuga á því hvernig ég debuggaði þetta þá keyrði ég 
    
-   "strace -ff -s 2048 nslookup [www.google.com](http://www.google.com/)" 
    
-   [11:40](https://advania.slack.com/archives/D03EJR3RTNK/p1664538029675279) 
    
-   sá svo þetta þar og elti þræðina: 
    
-   [11:40](https://advania.slack.com/archives/D03EJR3RTNK/p1664538031606999) 
    
-   [pid 1713618] <... futex resumed>)      = -1 ETIMEDOUT (Connection timed out) 
    
-   [pid 1713616] clone(child_stack=0x7f0693ffee70, flags=CLONE_VM|CLONE_FS|CLONE_FILES|CLONE_SIGHAND|CLONE_THREAD|CLONE_SYSVSEM|CLONE_SETTLS|CLONE_PARENT_SETTID|CLONE_CHILD_CLEARTIDstrace: Process 1713618 attached , parent_tid=[1713618], tls=0x7f0693fff700, child_tidptr=0x7f0693fff9d0) = 1713618 
    
-   [11:40](https://advania.slack.com/archives/D03EJR3RTNK/p1664538053032679) 
    
-   [pid 1713616] read(12, "search landskerfi.is\nnameserver 88.221.82.221\nnameserver 212.30.230.230\nnameserver 212.30.230.200\n", 4096) = 98 
    

Debug 

-   If the network is not functioning, check network card status. 
    
    -   ifquery networkcardname 
        
-   Turn it on 
    
    -   ifup networkcardname 
        
-   Turn it off 
    
    -   ifdown networkcardname 
        
    
-   netstat -tulpn 
    

-   netstat -tulpn | grep LISTEN 
    
-   netstat –an 
    
-   netstat -tnlp 
    
-   ss -an | less 
    
-   ss -tulpn 
    
-   ps -ef | grep webmin 
    
-   iptables -nvL 
    
-   systemctl status NetworkManager. 
    
-   nmcli dev connect ens160 
    
    -   To make it connect by default. 
        
    
    nmcli con mode ens160 connection.autoconnect yes 
    

-    ip -s link show 
    
    -   This show statistics for the link, dropped packages, etc.  
        
-   Sjá hvort incoming connection er að virka. 
    
    -   tcpdump -i any port 22 
        

atop -m 

[https://www.digitalocean.com/community/tutorials/atop-command-in-linux](https://www.digitalocean.com/community/tutorials/atop-command-in-linux) 

802.1x 

-   If you have issues with finding the certificate use sudo nm-connection-editor. 
    

[https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/networking_guide/sec-configuring_802.1x_security](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/networking_guide/sec-configuring_802.1x_security)