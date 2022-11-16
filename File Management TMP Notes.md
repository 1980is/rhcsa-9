## Change ownership

``chown john:john alamo``
This changes the owner and the group on the file/folder alamo.
If you just want to change the group you can do ``chown :john alamo``
You can also use the ``chgrp`` command. ``chgrp john alamo``

## Change permissions

-   0 No permission.
-   1 Execute permission.
-   2 Write permission.
-   3 Write and execute permissions.
-   4 Read permission.
-   5 Read and execute permissions.
-   6 Read and write permissions.
-   7 Read, write, and execute permissions.

This gives the owner full permission, group read and execute permission, and others no permission on "myfile".

``chmod 750 myfile``

This is known as the absolute mode. There is a relative mode that you can use. Let's say I wanted to make myfile executable.

``chmod +x myfile`` 




``