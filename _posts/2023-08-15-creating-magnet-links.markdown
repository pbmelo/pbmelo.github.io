---
layout: post
title:  "Creating torrent files and magnet links to share data with your friends"
date:   2023-08-15 22:26:00 -0700
categories: tutorials opinion
tags: torrent
---

## How to create a magnet link to share files with friends via torrent

This is a very short tutorial to a very good way of quickly sharing files with your friends.  I will share how to create and share magnet links via [ctorrent](http://localhost:4000/tutorials/2023/08/15/creating-magnet-links.html#h-alternative-1-ctorrent) and [transmission-cli](http://localhost:4000/tutorials/2023/08/15/creating-magnet-links.html#h-alternative-2-transmission-cli).  Click on the links to jump to the part of the post that matters.

## Why create a torrent instead of uploading it to a commercial cloud storage service?

If you went to a "higher education institution", you probably have an institutional e-mail and you can access two of the main cloud storage providers.  If you didn't, you still probably have had an account on one or both of them at some point of your life.  However, using them nowadays might be problematic.

Recently, Google has decided to severely limit its Drive storage for education institutions to ridiculously small amounts, and Microsoft's OneDrive also requires a mandatory two-factor identification using a 2FA key or a phone number, which raises privacy concerns.  Dropbox provides 2 Gb of storage, which is decent enough for most applications, but personal accounts do not have zero-knowledge encryption, so you would need to further encrypt your files yourself before the upload for them to be technically private.

You can definitely use commercial services offered by privacy-respecting companies, such as [Proton Drive][proton-drive], [NordLocker][nordlocker], [Tresorit][tresorit], [Sync.com][sync.com], [Mega][mega], or even better, host your own [Nextcloud][nextcloud] server.  But you will have to create an account for any of those, or set up your own server and open ports on your own network so your friends can have access to your data.  Personally, I prefer to keep the number of accounts I own to a minimum and not expose my self-hosted services to the internet.  True, I could give people a WireGuard key to connect to my home network, but it is pretty obvious why this isn't a great idea.

But here comes the most important reason of all: maybe you will have fun doing this via torrent and learn something new!

In summary, the whole process is very simple and consists of two steps:
1. Create a `.torrent` file;
2. Add it to your torrent client to seed it.

To create a torrent file, we will need the file or directory that we are sharing (obviously) and a tracker (optional).  [According to wikipedia][tracker-wiki], "a BitTorrent tracker is a special type of server that assists in the communication between peers using the BitTorrent protocol".  A list of trackers can be found online, for instance [here][trackerslist2] or [here][trackerslist1].

## Alternative 1, ctorrent

I got this set of instructions from Ask Ubuntu forums, [this post][askubuntu-question-ctorrent].

Just install ctorrent and run the following commands

```console
ctorrent -t -u "http://tracker.example.com:6969/announce" -s example.torrent file_or_dir_to_upload
```
to create your tracker and
```console
ctorrent example.torrent
```
to start seeding it.

Then share your file with your friends and they should be able to download it via torrent

## Alternative 2, transmission-cli

I got this set of instructions from Linux Config, [this post][linuxconfig-transmission].

Install [transmission-cli][transmission-git] and run

```console
transmission-create file_or_dir_to_upload -t udp://tracker.openbittorrent.com:80
```
to create your `.torrent` and
```console
transmission-remote -a file_or_dir_to_upload.torrent
```
to start seeding.

And voila!  Just send the file over to your friends.

## Converting torrent files into magnet links

To convert your `.torrent` file into a magnet link, just copy the output of the following command
```console
transmission-show -m yourfiles.torrent
```
and share it.  You can pipe it to `xclip` or a similar application and send it to someone as a text.

## Relevant links

The information below was typed on Aug 15th, 2023, so prices and storage limits might be out of date.  Regardless, it's worth it considering the following services:

1. [Proton Drive][proton-drive], €3.99/mo; 200 GB, Free; 1 GB
2. [NordLocker][nordlocker], $3.99/mo; 500 GB, Free; 3 GB
3. [Tresorit][tresorit], $10.42/mo; 200 GB, Free; 3 GB
4. [Sync.com][sync.com], $96/yr; 2 TB, Free; 5 GB
5. [Mega][mega], $5.45/mo; 400 GB, Free; 15 GB

[proton-drive]: https://proton.me/drive
[nordlocker]: https://nordlocker.com/
[tresorit]: https://tresorit.com/
[sync.com]: https://www.sync.com/
[mega]: https://mega.io/
[nextcloud]: https://nextcloud.com/
[askubuntu-question-ctorrent]: https://askubuntu.com/questions/32024/how-to-create-a-torrent-using-the-command-line
[linuxconfig-transmission]: https://linuxconfig.org/how-to-create-and-share-torrent-on-linux
[wasi-odyssey]: https://wasi0013.com/2018/10/21/how-to-create-a-torrent-file-in-linux/
[transmission-git]: https://github.com/transmission/transmission
[tracker-wiki]: https://en.wikipedia.org/wiki/BitTorrent_tracker
[trackerslist1]: https://github.com/ngosang/trackerslist
[trackerslist2]: https://www.theunfolder.com/torrent-trackers-list/