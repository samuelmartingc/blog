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

The solution has been simpler that I was expecting, just make snapshots of the current state in my SD card. I will show you how to make saves for your cards and how to recover them with simple commands in Linux.

**Where is located?**

First, we introduce the SD in our laptop where it will be saved. We will want to know the name of the SD in our system, you must type this command.

```bash
sudo fdisk -l
```

Usually it will be _/dev/sbd_ , the output should be something like this.

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

**Make copy to a local file**

Now we know where is allocated our card, the next step is to clone to a local file and compress it.
As you may want to save different snapshots, in this code, the name of the file will be the image(current_day).gz

```bash
sudo dd bs=4M if=/dev/sdb | gzip > /home/username/myImg`date +%d%m%y`.gz
```

This could take a long time, so be patient and take a coke :)

The output should be similar to this one, it took me 20 minutes.

```bash
3710+0 records in
3710+0 records out
15560867840 bytes (16 GB, 14 GiB) copied, 1208,12 s, 12,9 MB/s
```

**Restore it to your card**

Ok, suppose that we have finished some project or we have failed and we want to switch to the last week version.
As we have the snapshots saved as local files, we must only choose the correct one and burn it to our card.

```bash
sudo gzip -dc /home/username/myImg.gz | dd bs=4M of=/dev/sdb
```

Some people have said that another sudo command were required in his operative system, it the previous command fails to you, try with this one.

```bash
sudo gzip -dc /home/your_username/image.gz | sudo dd bs=4M of=/dev/sdb
```

This step will be probably taking more time than the previous one, because most of the cards have better performance reading than writing.

**Conclusion**

This post has been short enough to not waste your time reading unrelating things, I hope that you have find this commands useful. Have a good day :)
