
To see disks and partitions. ``lsblk``
If for some reason you don't think that is correct you can ``cat /proc/partitions`` 

## Mount

This command checks the "/etc/fstab" file is valid.
``findmnt --verify`` 

To mount all unmounted devices.
``mount -a``

*During the exam, reboot the machine to verify all mounts!*
If your system can't boot because of a problem with "/etc/fstab" you will fail the exam.



