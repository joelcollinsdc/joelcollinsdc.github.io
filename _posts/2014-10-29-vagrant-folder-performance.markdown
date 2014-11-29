---
layout: post
title:  "Vagrant Shared Folder (NFS / Rsync) Performance"
date:   2014-11-29
---

Disclaimer... I'm still learning vagrant & virtualization.

*tl;dr version*: If you need a large codebase accessible via your host, rsync isn't ready yet and nfs isn't lighting fast

I'm spending the thanksgiving weekend trying to get a drupal vm setup using vagrant.  After several past weekends failing to learn chef and docker I think I'm making some progress, but I'm getting stuck on sharing folders with the host.  One of the major goals of this project was to allow developers to utilize IDEs on their host, so I wanted the bulk of the codebase to be accessible from the host.  For the weekend, I'm on my macbook but ideally this setup would work on windows hosts as well.  Unfortunately I think I'm stuck.

At least in virtualbox, native shared folder performance is not acceptable for hosting the drupal profile that I want hosted.  (Depending on what is included, the codebase can be 50-100mb).  NFS sems acceptable, but not great.  Page load times are 5-10x slower than native.  I haven't been able to test smb yet but I presume its similar.

Rsync would seem like a good next step, as in theory the performance would be near native, but as of vagrant 1.6.5 there are [major issues](https://github.com/mitchellh/vagrant/issues/3249) with the rsync-auto job.  For now I'm considering either scraping this for now or looking at some ability to toggle between the codebase living inside the virtual for performance or living on the host for debugging/ide capability.  Another thing I wanted to explore was having the code live in the virtual but use nfs to mount it on the host.