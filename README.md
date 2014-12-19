ASUSWRT_Samba_Fixer
=============

Replace the default Samba smb.conf file with a customized configuration file, then kill and restart the smbd daemon. Designed to be run at boot time, on a router with an attached USB storage drive.


Out of the box, the Asus RT-AC87 router has some handy, but limited, file and media sharing capabilities. Connect a USB hard drive to one of its USB ports, and the router can share data from that drive with anyone on your network. The firmware implements Samba, but through the GUI you have only two options: allow anonymous guests complete access, or require a username and password for every connection. Samba can be configured far more granularly, but you cannot get there from the AC87 web interface. This script automates replacing the stock configuration file with one customized to the owner's preference.

Requirements:
=============

* Runs on an Asus wireless router using ASUSWRT firmware. This is known to work on the Asus RT-AC87U; it likely works on most other RT-XXXXX models running version 3.0.0.4 or newer. 
* This only works if a USB drive is attached

Usage: 
=============

Store fixsamba to /jffs on the router
chmod 755 /jffs/fixsamba

Modify smb.conf to suit your preference.
Store smb.conf to /jffs
chmod 644 /jffs/fixsamba

```
nvram set script_usbmount="/jffs/fixsamba"
nvram commit

```

Upon either rebooting, or disconnecting / reconnecting the USB drive, the script will execute, kill all existing smbd processes, copy the custom configuration file into place, and restart smbd with the custom conf file.