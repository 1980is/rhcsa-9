# File Management

``chgrp`` changes the group. E.g., chgrp documents aslaug.


## ACL

ACL's are not a part of the RHCSA 9 but I still wrote down information about it.

-   There are two types of ACL. 
    
    -   The normal ACL. 
        
    -   The default ACL. 
        
-   To create an ACL list you use the command setfacl. 
    
-   setfacl -R -m g:sales:rx filename 
    
-   Setfacl -m d:g:profs:rx foldername/ 
    
    -   This sets the group profs as a default group that can read and execute all files creating in foldername in the future. 
        
-   If fileacl not supported message appears, there is something wrong in the filesystem. 
    

-   getfacl foldername     
    

SUID, SGID, and Sticky Bit 

-   chmod to set SUID, SGID, and Sticky Bit. 
    
    -   To apply SUID, SGID, and sticky bit, you can use chmod as well. SUID has numeric value 4, SGID has numeric value 2, and sticky bit has numeric value 1. 
        

-   SUID = 4 
    
    -   Files, run as user. 
        
    -   Dangerous! 
        
    -   SUID on directories has no meaning. 
        
    -   Never use. 
        
    -   chmod u+s filename 
        
        -   This enables set user id for that file. If Root is the owner. 
            
    -   To see if the SUID bit is set the permissions has a capital S. 
        
        -   -rwSr--r-- 
            
-   SGID = 2 
    
    -   Run as group owner. 
        
    -   It inherits DIR group owner when new files are created. It can good in shared environments. 
        
    -   chmod g+s /foldername 
        
        -   This enables set group id for that folder.  
            
    -   Dangerous! 
        
    
-   STICKY = 1 
    
    -   Sticky bit has no meaning on files but it does have meaning on directories. 
        
    -   It makes it so that that delete only works if the owner deletes. 
        
    -   chmod +t * 
        
        -   This applies a sticky bit to all filed in the current directory. 
            
        -   To see if the Sticky Bit is set the permission has a capital T at the end. 
            
            -   -rw-r--r-T