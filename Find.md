# Find

## By size 

-   find / -type f -size +100M 
-   find /etc/ -type f -size -1000c 
    -   c is for smaller than. 

---

## Folder or file 

-   find ~ -type d -name "Music" 
   
---

## Copy found items

-   find /etc/ -name "hosts" -exec cp {} /tmp \\;

--- 