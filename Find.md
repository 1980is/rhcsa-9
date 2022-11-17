# Find

## By size 

-   find / -type f -size +100M 
-   find /etc/ -type f -size -1000c 
    -   c is for smaller than. 

---

## Folder or file 

``find ~ -type d -name "Music"``
This finds a directory named "Music".

``find / -name linux.conf``
This searches everything for a file named "linux.conf".
   
---

## Copy found items

-   find /etc/ -name "hosts" -exec cp {} /tmp \\;

--- 