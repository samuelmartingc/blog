+++
title = "Saving snapshots for SD card"
description = "Saving snapshots for SD cards to restore information or cloning them"
tags = [
    "development",
    "raspberry",
]
date = "2017-01-22"
categories = [
    "Development",
]

image = "raspberry.png"

toc = true # optional, When set to TRUE this parameter, table of contents appears in only this article.
+++

**Introduction**

Now that I am playing with my Raspberry Pi, I need to use different SD cards for many projects, and I was bored of formatting again and again my card, so I were searching for a more efficient way to switch between my projects and also having backups in an easy way.

The solution has been simpler that I was expecting, just make snapshots of the current state in my SD card. I will show you how to make backups for your cards and how to restore them with simple commands in Linux.

**Where is located?**

First, we will insert the SD card in the computer where we will save the backup. We will want to know the name of the SD card in our system. To do this, you can type this command:

```bash
sudo fdisk -l
```

Usually it will be `/dev/sdb`. The output should look like this:

```bash
Disk /dev/sdb: 14,5 GiB, 15560867840 bytes, 30392320 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x1aaa6849

Device     Boot  Start      End  Sectors  Size Id Type
/dev/sdb1         2048   499711   497664  243M  c W95 FAT32 (LBA)
/dev/sdb2       501760 30392319 29890560 14,3G 83 Linux
```

**Making a disk image of your SD card**

Now we know where is located our card, the next step is to clone it to a (compressed) disk image. Basically, we are copying all the contents of the SD card to a file. This proccess is very similar to the creation of an ISO file from any DVD.

As you may want to save different snapshots, in the example command below, we will add the timestamp to the file, so its name will be `image-DDMMYYYY-epochtime.gz` (where *DD*, *MM* and *YYYY* are the day, the month and the year and *epochtime* is the time in seconds elapsed since 1 January 1970). This will save you from overwriting a backup accidentally.

```bash
sudo dd bs=4M if=/dev/sdb | gzip > /home/$USER/image-$(date +%d%m%Y)-$(date +%s).img.gz
```

This could take a long time, so be patient and take a walk in the meanwhile :)

The output should be similar to this one, it took 20 minutes to finish:

```bash
3710+0 records in
3710+0 records out
15560867840 bytes (16 GB, 14 GiB) copied, 1208,12 s, 12,9 MB/s
```

**Write the disk image to the SD card**

Ok, let's suppose that we have finished some project or we have failed and we want to rollback the SD card to the backup of the last week. We will do the inverse process. Following with the explaination above, this is conceptually similar to burning an ISO file to any DVD.

We must simply choose the right disk image and burn it to the SD card.

```bash
gzip -dc /home/$USER/image-DATE-seconds.img.gz | sudo dd bs=4M of=/dev/sdb
```

This step will probably take more time than the previous one, because most of the cards have better performance reading than writing.

**Seeing the progress of `dd`**

Yes, is tiresome to look at `dd` without knowing the progress, but you can run the following command in another terminal to stay informed:

    progress -m
    
 In older systems, you can use this alternative that will trigger a progress notification on the terminal used by `dd`:
 
     while true; do sudo killall -USR1 dd; sleep 1; done

**Conclusion**

This post has been short enough to not waste your time reading unrelated things, I hope that you have find these commands useful. Also, if you didn't guess it yet, you can apply the same procedure to USB flash drives, microSD cards and hard disks if you have enough space.

Have a good day :)
