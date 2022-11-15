# Users and Groups
---

## Users 

### Adding users
``useradd -D`` to specify default settings. 

Files in /etc/default/useradd apply to useradd only.  
Alternatively, write default settings to /etc/login.defs This is the main settings config file.

Changing this will not affect previously created users, only users that will be created in the future.

Files in /etc/skel are created to the user home directory upon creation. If we want to send a message, scripts, etc. We can use /etc/skel.

---

### Managing users

#### Passwords
To view password settings for user John.
``chage -l john``

To set password options for John.
``chage john``

You can also view the passwd options in /etc/shadow. You can see if the user account is locked out. The second field is the password hash. If the password hash starts with ! The user account is locked out. 
\
If you want to transfer a password from another server to the next one, simply copy the password hash in /etc/shadow from the server with the correct password and paste it into field number 2.
\
To lock a user account.
``usermod -L john``
\
To unlock an account.
``usermod -U john``
\
See previous logged in users.
``last``
\
See currently logged in users.
``w`` or ``who``.
To edit /etc/passwd use vipw. Do not edit the file directly.   

/etc/profile: Used for default settings for all users when starting a login shell  

/etc/bashrc: Used to define defaults for all users when starting a subshell  

~/.profile: Specific settings for one user applied when starting a login shell  

~/.bashrc: Specific settings for one user applied when starting a subshell 

Move password from old shadow to new shadow file. 

-   First create the new user and give him a tmp password. Copy the old hash from the old shadow file to the new one. 
    

## Groups

-   groupadd newgroup 
    
-   chgrp changes the group. E.g., chgrp documents aslaug. 
    
-   groupmems -g sales or lid -g groupname 
    
-   Use vigr to change the /etc/groups file. 
    
-   groups armann 
    
    -   First group is the primary group. 
        
    -   You can use newgrp sales to change the primary group to sales. 
        
    -   This is only a temporary primary group change, when you exit, it's back to your original primary group. 
        

SUDO 

-   getent group sudo/wheel 
    
-   usermod -aG sudo username