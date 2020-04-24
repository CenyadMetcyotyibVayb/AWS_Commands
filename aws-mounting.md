```
sudo lsblk --output NAME,TYPE,SIZE,FSTYPE,MOUNTPOINT,LABEL

NAME    TYPE SIZE FSTYPE MOUNTPOINT LABEL
xvda    disk   8G                   
└─xvda1 part   8G xfs    /          
xvdf    disk  30G                   
└─xvdf1 part  30G xfs             
```

```
mount /dev/xvdf1 /mnt/xvdf/ -t ext4
mount: wrong fs type, bad option, bad superblock on /dev/xvdf1,
       missing codepage or helper program, or other error

       In some cases useful info is found in syslog - try
       dmesg | tail or so.

mount /dev/xvdf /mnt/xvdf/ -t ext4
mount: wrong fs type, bad option, bad superblock on /dev/xvdf,
       missing codepage or helper program, or other error

       In some cases useful info is found in syslog - try
       dmesg | tail or so.
```


```
fdisk -l /dev/xvdf

Disk /dev/xvdf: 32.2 GB, 32212254720 bytes, 62914560 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk label type: dos
Disk identifier: 0x000123f5

    Device Boot      Start         End      Blocks   Id  System
/dev/xvdf1   *        2048    62910539    31454246   83  Linux
```

```
dmesg | tail
[  497.636734] EXT4-fs (xvdg1): mounted filesystem with ordered data mode. Opts: (null)
[  497.640565] SELinux: initialized (dev xvdg1, type ext4), uses xattr
[  629.584587] EXT4-fs (xvdf1): VFS: Can't find ext4 filesystem
[  633.616627] EXT4-fs (xvdf): VFS: Can't find ext4 filesystem
[  643.570436] EXT4-fs (xvdf1): VFS: Can't find ext4 filesystem
[  682.903250] XFS (xvdf1): Filesystem has duplicate UUID ef6ba050-6cdc-416a-9380-c14304d0d206 - can't mount
[  799.584731] XFS (xvdf1): Filesystem has duplicate UUID ef6ba050-6cdc-416a-9380-c14304d0d206 - can't mount
[  837.470871] XFS (xvdf): Invalid superblock magic number
[  842.906243] XFS (xvdf1): Filesystem has duplicate UUID ef6ba050-6cdc-416a-9380-c14304d0d206 - can't mount
[  892.907414] XFS (xvdf1): Filesystem has duplicate UUID ef6ba050-6cdc-416a-9380-c14304d0d206 - can't mount
```

```
mount -o nouuid /dev/xvdf1 /mnt/xvdf/
```

```
xfs_admin -U generate /dev/xvdf
```