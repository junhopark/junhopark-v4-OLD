---
title: Replacing SSD in MacBook Air (13" mid-2012)
layout: posts
---

I was running low on my 13" mid-2012 MacBook Air's SSD, which had me pretty concerned.  Thankfully I recently discovered that the SSD inside this thing is replaceable.  After some Googling, my SSD options came to [OWC Aura 6G](https://eshop.macsales.com/shop/ssd/owc/macbook-air/2012) and [Transcend JetDrive](https://www.amazon.com/gp/product/B00JQXT5RG).  I spotted more negative reviews with the OWC drive Vs. the Transcend drive so in the end, I decided to go with Transcend and get the 960 GB version.  It cost me $448.59 on Amazon.

Once I received the drive, replacing it was super easy and took me about 5 minutes.  I'm not going to go into details on how to replace the drive because that's very easily Google-able.  FYI, I "cloned" my drive using my Time Machine backup, which was being backed up on my Synology NAS.  I've used Time Machine backup in cloning the contents of a SSD a few times in the past and it works really well.

I did want to point out the following gotchas:

1) This was my first time having to restore from a Time Machine backup that's *stored on a network drive*.  From the OS X Recovery Screen (you get there by holding Command + R when your machine is starting up, by the way) my laptop wasn't able to connect to my Synology NAS.  I am not 100% sure if this is the thing that fixed this issue but after I mounted the drive in the following way via Terminal...:

    cd /Volumes
    mkdir junho-mba-backup
    mount_afp -i afp://192.168.1.9/junho-mba-backup junho-mba-backup

I was able to successfully connect to my Synology device and retrieve the Time Machine backup.

2) After my files were restored on the new SSD, I noticed that FileVault (*System Preferences > Security & Privacy > FileVault*) was turned off (on my original SSD it was turned on).  I like my drives encrypted at all times.  Anyhow, when I attempted to turn it on, I got the following error message:

FileVault can't be turned on for the disk "Macintosh HD".
Some disk formats don't support the recovery partition required by encryption.  To use encryption, reinstall this version of Mac OS X on a reformatted disk.

After a little bit of Googling, I came across numerous solutions, most of which seemed overly complex and even risky.  Thankfully, [the simplest solution I moved forward with](http://karl.kranich.org/2014/06/14/solved-how-to-recreate-the-recovery-partition-on-osx-mavericks-after-a-time-machine-restore-to-a-blank-drive/) ended up working out for me (hooray!).  I downloaded OS X El Capitan from the Apple App Store (note: it will save the file in your /Applications folder) and then went to [http://musings.silvertooth.us/downloads-2/](http://musings.silvertooth.us/downloads-2/) to download the Recovery Partition Creator (I clicked on the link to: Recovery Partition Creator 4.x).  When I ran Recovery Partition Creator, all I had to do was to tell where the downloaded OS X El Capitan file is located.  Once this was done, I was able to FileVault back on.

3) When I attempted to open a document in Microsoft Word, I was prompted for the Office product key, which was completely unexpected.  Thankfully, I was able to find the product key.

My laptop's been running with the new SSD for about 5 days now and it's been running just as well as before the SSD swap.  According to the Blackmagic Disk Speed Test app, it appears that the new drive is faster.

BEFORE:
![](/assets/img/disk_speed_test_before_2016-07-13-1936.png)

AFTER:
![](/assets/img/disk_speed_test_after_2016-07-15-630.png)

By the way, when I had opened up my MacBook Air, I discovered that the battery is easily swappable as well.  Exciting discovery!
