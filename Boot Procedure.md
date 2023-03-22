# Boot Procedure

## Grub
The location of Grub depends upon if you boot using BIOS system or en EFI system. To know if you are on a BIOS or EFI system. ``dmesg | grep "EFI"``. If you get nothing you booted using BIOS. You can ``dmesg | grep "BIOS"`` just to be sure. 
Another way is to use ``lsblk`` and if your boot disk is mounted on "/boot" than you are using BIOS.
If it says "/boot/efi". You guessed it, you are using EFI. :)

You need to edit the configuration file in "/etc/default/grub" to make changes persistent. Afterwards you must compile the changes to **grub.cfg**. You cannot edit that file directly.

### For BIOS/MBR

To make static changes to Grub edit "/etc/default/grub".
Commit the changes you make. ``grub2-mkconfig -o /boot/grub2/grub.cfg``

### For EFI

To make static changes to Grub edit "/etc/default/grub". Commit the changes you make. ``grub2-mkconfig -o /boot/efi/EFI/redhat/grub.cfg``

## Systemd Targets

- emergency.target
  - Used for troubleshooting in a minimal environment.
- rescue.target
  - Also used for troubleshooting but not in a minimal environment.
- multi-user.target
  - The default environment, without a GUI.
- graphical.target
  - A fully functioning target like multi-user.target but with a GUI.

To know what target you are in do ``systemctl get-default``. You can also do ``systemctl list-dependencies``
Since I'm in the grapical.target, it lists first the default.target and then underneath it is multi-user.target.

### Change the default systemd target

Let's set the default to a non GUI target. ``systemctl set-default multi-user.target``
You must reboot the machine to enter the new default target.

### Change a running target

Let's say we are running in a multi-user.target (GUI) and we want to
switch to a non-graphical target we run this command. ``systemctl isolate multi-user.target``
Once we are done and we want to get back to the GUI we issue``systemctl set-default multi-user.target``

### Change a target during boot in Grub

Add this the end of the linux line. ``systemd.unit=emergency.target`` You can use any of the targets I listed before instead of emergency.


