# Find / Search

How to search.

find \[/path/to/directory] \[search_parameters]
If you don't specify a directory, it searches the working directory.

## By size 

Find files that are larger than 100M.
``find / -type f -size +100M``

Find tiles that are smaller than 1000 bytes.
``find /etc/ -type f -size -1000c`` 

## Folder or file 

Find a directory named "Music" in your home directory.
``find ~ -type d -name "Music"``

This searches everything for a file named "linux.conf".
``find / -name linux.conf``
   
## Copy found items

Find all files under "/etc" named hosts and copy them to "/tmp".
``find /etc/ -name "hosts" -exec cp {} /tmp \\;``

## By date and time

Find all files that have been modified in the last minute in the "dev" directory.

``find /dev/ --mmin -1``

``
