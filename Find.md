# Find / Search

How to search.

find \[/path/to/directory] \[search_parameters]
If you don't specify a directory, it searches the working directory.

## General commands

### Or operator
``find -name stallone -o -name brucewillis``

Use -o as an "or" operator to find either stallone or brucewillis.

### Don't find something

To find everything except something. Let's search for everything excepts something that starts with an "f".

find -not -name "f*"

## Search for by permissions

Find files with exactly 664 permissions.
``find -perm 664``

Find files with at least 664 permissions.
``find -perm -664``

Find files with any of these permissions.
``find -perm /664``

## By size 

The following options exist for size.
1. Bytes = c
2. Kilobytes = k
3. Megabytes = M
4. Gigabytes = G

Find files that are larger than 100M.
``find / -type f -size +100M``

Find tiles that are smaller than 1000 bytes.
``find /etc/ -type f -size -1000c`` 

## Folder or file 

Find a directory named "Music" in your home directory.
``find ~ -type d -name "Music"``

This searches everything for a file named "linux.conf".
``find / -name linux.conf``

Find both "bear" and "Bear".
``find -iname bear``
   
## Copy found items

Find all files under "/etc" named hosts and copy them to "/tmp".
``find /etc/ -name "hosts" -exec cp {} /tmp \\;``

## By date and time

### Find modified within a timeframe
Find all files that have been modified in the last five minutes in the "dev" directory. Think about "mm" as "modified minute". The latter command finds everything that was modified **more** than five minutes ago.

``find /dev/ -mmin -5``
``find /dev/ -mmin +5``

To search for modified files in 24 hour blocks. This command finds all files modified in my "Documents" directory in the last 24 hours. 0 stands for the last 24 hours. 1 stands for between 24-48 hours and so on.

``find Documents/ -mtime 0``

## By change time - metadata e.g., permissions

Modification time reflects when something is created or edited.
**Change time is not modified time.** 

Change time reflects changed Metadata. For example if someone changes the permission. We can find that information with the following command. This finds all changed metadata within the last 5 minutes in the Documents directory.

``find Documents/ -cmin -5``

