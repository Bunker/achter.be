+++
author = "Bunker"
categories = ["raspberry pi", "backup", "arch linux", "rsync", "linux"]
class = "post"
date = "2015-11-12T01:53:50+01:00"
draft = false
tags = ["raspberry pi", "backup", "arch linux", "rsync", "linux"]
title = "Boot Arch Linux from USB on Raspberry Pi 2"
type = "post"

+++

At the moment I'm setting up a backup system in Arch Linux and minimise the risk of sd-card corruption, I'm going to run the OS from a usb stick (you can also use an usb drive if you want). I'm using [this guide][1] as a basis. It's meant for Raspbian, but I adapted the procedure below to Arch linux.

In the guide above we are going to follow the extended procedure. Because that way we are sure that every time we boot we have the correct stick.

To make sure our stick is recognised by Arch we run lsblk

you should see something similar like this:

```
   NAME        MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
   sda           8:0    1  7.6G  0 disk 
   `-sda1        8:1    1  7.6G  0 part 
   mmcblk0     179:0    0  3.7G  0 disk 
   |-mmcblk0p1 179:1    0  100M  0 part 
   `-mmcblk0p2 179:2    0  3.6G  0 part /
```

The drive we want in my case the sda drive. Make note we are going to need that drive name.

Let us first install gdisk 

    sudo pacman -S gdisk

once that finishes, we are going to use gdisk on the usb stick.

    sudo gdisk /dev/sda

Enter d to delete partion(s).

Enter n to create a new primary partition (number 1) and use the full capacity by hitting return a few times until done
*note*: if you want more partitions use +xxxM to create a different size and repeat n till there is no space left or you have your number of partitions

Now write the new information to the stick by entering "w"

You should get something like this output

```
  Command (? for help): d
  Using 1
  
  Command (? for help): n
  Partition number (1-128, default 1): 
  First sector (34-15826910, default = 40) or {+-}size{KMGTP}: 
  Last sector (40-15826910, default = 15826910) or {+-}size{KMGTP}: 
  Current type is 'Linux filesystem'
  Hex code or GUID (L to show codes, Enter = 8300): 
  Changed type of partition to 'Linux filesystem'
  
  Command (? for help): w
  
  Final checks complete. About to write GPT data. THIS WILL OVERWRITE EXISTING
  PARTITIONS!!
  
  Do you want to proceed? (Y/N): y
  OK; writing new GUID partition table (GPT) to /dev/sda.
  The operation has completed successfully.
```
Now repeat the gdisk command and use i

    sudo gdisk /dev/sda

you'll get an output like:

```
  Using 1
  Partition GUID code: 0FC63DAF-8483-4772-8E79-3D69D8477DE4 (Linux filesystem)
  Partition unique GUID: 0ED53DE0-0BD6-4F15-AC97-A4D0494CEF18
  First sector: 40 (at 20.0 KiB)
  Last sector: 15826910 (at 7.5 GiB)
  Partition size: 15826871 sectors (7.5 GiB)
  Attribute flags: 0000000000000000
  Partition name: 'Linux filesystem'
```

The Partition unique GUID is the one we need, in the next step:

    sudo cp /boot/cmdline.txt /boot/cmdline.txt.old

let's copy the original cmdline.txt file and edit it:

    sudo nano /boot/cmdline.txt

replace the root=/mnt/... with root=PARTUUID=youruniqueidentifier

```
  root=PARTUUID=0ED53DE0-0BD6-4F15-AC97-A4D0494CEF18 rw rootwait console=ttyAMA0,115200 console=tty1 selinux=0 plymouth.enable=0 smsc95xx.turbo_mode=N dwc_otg.lpm_enable=0 kgdboc=ttyAMA0,115200 elevator=noop
```
We now continue with formatting, mounting, installing rsync (which we use later on again as backup system) and the mirroring

```
   sudo mke2fs -t ext4 -L rootfs /dev/sda1
   sudo mount /dev/sda1 /mnt
   sudo pacman -S rsync
   sudo rsync -axv / /mnt
```

Now we need to get a unique identifier for the fstab drive information:

    sudo tune2fs -l /dev/sda1

You get a lot of info, but the most important part is the Filesystem UUID

```
  Filesystem volume name:   rootfs
  Last mounted on:          /mnt
  Filesystem UUID:          b8389d09-e7a6-4358-9501-9a309938d30d
  Filesystem magic number:  0xEF53
  Filesystem revision #:    1 (dynamic)
```

Next we can enter the information into the filesystem table, /etc/fstab (on the stick, not the SD card). Add the following line:

```
   /dev/disk/by-uuid/b8389d09-e7a6-4358-9501-9a309938d30d    /   ext4    defaults,noatime  0       1
```

That should be it, try to reboot now, if it boots, type lsblk if you see a / under MOUNTPOINT next to your usb drive, it means you are running from the usb.

```
   NAME        MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
   sda           8:0    1  7.6G  0 disk 
   `-sda1        8:1    1  7.6G  0 part /
   mmcblk0     179:0    0  3.7G  0 disk 
   |-mmcblk0p1 179:1    0  100M  0 part 
   `-mmcblk0p2 179:2    0  3.6G  0 part
```

[1]: https://www.raspberrypi.org/forums/viewtopic.php?f=29&t=44177