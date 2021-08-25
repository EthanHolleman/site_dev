---
title: "How to actually connect to UC Davis campus wifi (Eduroam) on Linux"
date: 2021-08-19
tags: ["blogs", "Davis guides", "Linux"]
draft: false
---

 
I use Ubuntu 20.04 as my daily driver operating system at work and
at home. Until recently, when I was on campus I had a really hard time consistently
connecting to the Eduroam network on my Linux machine; usually
resorting to guest wifi (disgusting) and requesting a new login every two
weeks after my credentials expired.
 
A few days ago I decided I was going guest wifi cold turkey and returned to
by search for any resources that might be available. The [Davis IT knowledge hub](https://servicehubtest.ucdavis.edu/servicehub/?id=ucd_kb_article&sys_id=4c3c77664f83f2409cab76601310c767)
suggests you run a Eduroam provided Python script configuration program.
This worked on one of my machines and failed on another. Additionally, it
may require storing your password in plain text (don't do this). I had much
better luck following [this guide](https://ithelp.physics.ucdavis.edu/kb/linux-wireless-connection-issues-eduroam-and-moobilenetx)
from the physics department. However it is outdated and there is one key 
change you **must** make for the instructions in this guide to work.
 
The guide instructs you to use a file located at `/etc/ssl/certs/AddTrust_External_Root.crt` as
your CA certificate when configuring the connection. Unless you have an older
machine this file will probably not exist. This is because this particular certificate
expired in [May 2020](https://calnetweb.berkeley.edu/calnet-technologists/incommon-sectigo-certificate-service/addtrust-external-root-expiration-may-2020)
and has been updated. Instead, make sure to use the certificate located at
`/etc/ssl/certs/USERTrust_RSA_Certification_Authority.pem`. This path may be slightly
different if you are using a different distro. Follow all other instructions
provided by the physics department.
 
Hope this is helpful!


 
 
 
 

