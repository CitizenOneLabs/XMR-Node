![PiNode-XMR logo](https://github.com/monero-ecosystem/PiNode-XMR/blob/master/Screenshots/PiNode-XMR%20logo.jpg)
# User Manual v4.21.01-Open-Build		
#### Self Install Open Source Build for Raspbian (Raspberry Pi) & Armbian Debian Buster (For all other devices)
or
#### Pre assembled disk images available for download (Raspberry Pi 3b+ & 4)

## Support

* [Redit.com/r/PiNode](https://www.reddit.com/r/pinode/)
* Telegram group PiNode-XMR [t.me/PiNodeXMR](https://t.me/PiNodeXMR)

*Hosting large image files such as the pre-sync'd version does come with it's costs. If you like the project or found the images helpful any contribution would be gratefully received:*

43HoAhqx9q3MR1crAjpQtYVhvzQhZgqPwSWVQMmPvYmr18qVUEjCHcsEasuCxS486rWSSg1gbGqanet67NWRsh1bQL9KkB9

## Intro

Let me start by saying I'm glad the internet has bought you to here. It's taken several years to get to this point of the project, which in itself has been part of a multi year hobby creating nodes for cryptocurrencies and producing guides for beginners to follow along the way. The project is in a changing state at the moment with a shift from pre-built disk images, to you the user running a single command to initiate the install from this github repository. The reason for this change is to present the project as open source, increase transparency and trust. It also gives the added benefit of no longer being tied to the hardware of the device I was building the disk images on. This gives you the user much greater freedom to install your node on any Armbian device of your choice. Whilst this transition to open source finalises I will continue to provide the pre-made and pre-syncd disk images for the Raspberry Pi, but will phase this out over the year.
Also throughout the years I've had many requests from users if they could purchase pre-made nodes and although this is not something my lifestyle can accommodate, it does signal that users too have busy lifestyles, they want a node fast and I hope this project is a reasonable solution to that request.

To that end I hope you find this latest project invaluable to running your own Monero node, fast. The initial sync will take some time, and for that reason I also supply this node pre-sync'd as an image. Security for the device has been configured but every copy of this device currently has the same password as I set it. It is important you change it to something unique, this is detailed later on in this document.

Dan

*This Manual is still aimed at a low beginner level user including SD formatting and image writing. After these chapters and node usage you'll find detailed breakdowns of how this node works for those that are interested in contributing. Finally all suggested software used in the setup stages are downloadable for free*

## Contents:

* [Intro](https://github.com/monero-ecosystem/PiNode-XMR#intro)
   * [Features List](https://github.com/monero-ecosystem/PiNode-XMR#features)
   * [Hardware Requirements](https://github.com/monero-ecosystem/PiNode-XMR#hardware-requirements)
   * [Installing - Open Source (option 1)](https://github.com/monero-ecosystem/PiNode-XMR#installing)
      * [Raspberry Pi Self Install](https://github.com/monero-ecosystem/PiNode-XMR#raspberry-pi)
      * [Installing on all other devices - via Armbian Debian Buster OS](https://github.com/monero-ecosystem/PiNode-XMR#all-other-devices---armbian-debian-buster-os)
   * [Download - Pre-Configured Disk Image (option 2)](https://github.com/monero-ecosystem/PiNode-XMR#downloads)
   * [Setup](https://github.com/monero-ecosystem/PiNode-XMR#setup)
* [Web-UI: Getting started & General Usage](https://github.com/monero-ecosystem/PiNode-XMR#web-ui-starting-your-node-and-general-usage)
   * [Welcome Page](https://github.com/monero-ecosystem/PiNode-XMR#welcome-page--)
   * [Advanced Settings & Starting Monero](https://github.com/monero-ecosystem/PiNode-XMR#advanced-settings---starting-monero)
   * [Node Status](https://github.com/monero-ecosystem/PiNode-XMR#node-status--)
   * [Monero Blockchain Explorer](https://github.com/monero-ecosystem/PiNode-XMR#monero-blockchain-explorer)
   * [Transaction Status](https://github.com/monero-ecosystem/PiNode-XMR#transaction-status)
   * [Connection Status](https://github.com/monero-ecosystem/PiNode-XMR#connection-status)
   * [Log](https://github.com/monero-ecosystem/PiNode-XMR#log)
* [Web Terminal: Main System Menu](https://github.com/monero-ecosystem/PiNode-XMR#web-terminal--main-system-menu)
     * [System Settings](https://github.com/monero-ecosystem/PiNode-XMR#system-settings)
       * [Raspi-Config](https://github.com/monero-ecosystem/PiNode-XMR#raspi-config---hardware-management)
       * [Master Login Password set](https://github.com/monero-ecosystem/PiNode-XMR#master-login-password)
       * [Monero RPC password and user name set](https://github.com/monero-ecosystem/PiNode-XMR#monero-rpc-password-and-username)
       * [USB Storage setup](https://github.com/monero-ecosystem/PiNode-XMR#usb-storage-setup)
       * [SDCard Health Checker - via "Agnostics"](https://github.com/monero-ecosystem/PiNode-XMR#agnostics---sd-card-health-checker)
     * [Update Tools](https://github.com/monero-ecosystem/PiNode-XMR#update-tools)
       * [Update Monero](https://github.com/monero-ecosystem/PiNode-XMR#update-monero)
       * [Update PiNode-XMR](https://github.com/monero-ecosystem/PiNode-XMR#update-pinode-xmr)
       * [Update Blockchain Explorer](https://github.com/monero-ecosystem/PiNode-XMR#update-block-explorer)
       * [Update background system dependencies](https://github.com/monero-ecosystem/PiNode-XMR#update-background-system-dependencies)
     * [Node Tools](https://github.com/monero-ecosystem/PiNode-XMR#node-tools)
       * [Start/Stop Blockchain Explorer](https://github.com/monero-ecosystem/PiNode-XMR#startstop-blockchain-explorer)
       * [Prune Node](https://github.com/monero-ecosystem/PiNode-XMR#prune-node)
       * [Pop Blocks](https://github.com/monero-ecosystem/PiNode-XMR#pop-blocks)
     * [Extra Network Tools](https://github.com/monero-ecosystem/PiNode-XMR#extra-network-tools)
       * [Install tor](https://github.com/monero-ecosystem/PiNode-XMR#install-tor)
       * [View tor NYX - (network monitor)](https://github.com/monero-ecosystem/PiNode-XMR#tor-nyx)
       * [Install PiVPN](https://github.com/monero-ecosystem/PiNode-XMR#install-pivpn)
       * [Install No-IP (Dynamic DNS)](https://github.com/monero-ecosystem/PiNode-XMR#noipcom-dynamic-dns)
  
* [A note on tor](https://github.com/monero-ecosystem/PiNode-XMR#tor)
* [Connecting a Wallet -LAN](https://github.com/monero-ecosystem/PiNode-XMR#connecting-a-wallet---lan)
  * [Monero GUI](https://github.com/monero-ecosystem/PiNode-XMR#monero-gui)
  * [Monerujo app](https://github.com/monero-ecosystem/PiNode-XMR#monerujo-app)
* [Connecting a wallet - External Connections](https://github.com/monero-ecosystem/PiNode-XMR#connecting-a-wallet---external-connections)
  * [IP address considerations](https://github.com/monero-ecosystem/PiNode-XMR#ip-address-considerations)
  * [Port Forwarding](https://github.com/monero-ecosystem/PiNode-XMR#port-forwarding)
  
## Features:
* 5 Node modes (click to start)
  * Private Node
  * tor bridging Node - routes your transactions through the tor network
  * I2P bridging Node - routes your transactions through the I2P network
  * Public Node - Using new RPC payment feature
  * Private Node - with mining (For education/experiment only)
* Simple control with Web-UI
  * View Monero node and hardware status
  * Control bandwidth, connection limits and RPC port
  * Transaction pool and summary viewer
  * View connected peer info
  * Monerod log file view page
* Monero Block Explorer [Github - onion-monero-blockchain-explorer](https://github.com/moneroexamples/onion-monero-blockchain-explorer)
* Easy setup menu for config of passwords and Updates.
* **New** - Additional tools
  * raspi-config (Hardware and Wifi settings pre-built into PiNode-XMR menu
  * Agnostics - SD Card read/write health checker included
  * PiVPN - Tool for easy configuration of OpenVPN for Raspbian and Armbian
  * Pop blocks - Monero tool to help recover blockchain problems - UI
  * Systemd Monitor to track running node and explorer functions
  * tor installer - tor is no longer included and running as default due to censorship, political or legal restriction of users host country. Simple select to install and activate on user request.
  * All status boxes have improved scripts for clearer more constant feedback during high CPU loads.
  * Improved helper to setup an external USB storage device to hold the Monero blockchain. This new script allows a user to import a blockchain already held from a PC. Also on SD card failure this storage device can be identified by PiNode-XMR as configured for use, preserving the blockchain and so reducing re-startup time.
* All the other benefits of running a node on a Single Board computer (EG. RasPi, silent/fan-less, low power (approx 15w) for 24/7 node, low cost)
* Headless (No need for extra monitor,keyboard,etc) direct connect via Ethernet or WiFi**


**Connection via Ethernet required to configure WiFi

## Hardware requirements:

**For full hardware support view the [PiNode-XMR Hardware Wiki](https://github.com/monero-ecosystem/PiNode-XMR/wiki/Hardware)**

General
1. * Raspberry Pi 3/4 (incl B&+ models) for Pre-Configured disk image
   * Any ARM device that supports Armbian Debian OS for self install. *2GB RAM required for Monero source compile, but there is a work around* 
2. 8GB MicroSD Card with aditional min 100GB USB storage device for Monero Blockchain. Or 128GB MicroSD to store all-in-one.
3. Ethernet connection (can be replaced by WiFi after config, hardware dependant)


A final point on the hardware. This node is designed to be used 'headless'. The HDMI cable, mouse and keyboard is not required. This should allow you to tuck the node away somewhere and all interactions can be made with a device (pc or mobile) that is connected to the same network (your home one in most cases).


## Installing
### Self Install scripts
This project can now self install on top of an Armbian Debian OS in an effort to become completely Open Source (my disk images require you to trust me). This is a better alternative for everyone.

**Important - this project is intended to convert your device into a dedicated Monero node from a clean OS. Running this script on top of anything else existing on the device will likely overwrite it in an unrecoverable manner**

![PiNode-XMR landing page](https://github.com/monero-ecosystem/PiNode-XMR/blob/master/Screenshots/OS-Select.png)

### Raspberry Pi
Install your Raspbian OS as usual but ensure to install the "Minimal/Lite" version (No GUI) and ideally SSH into it as user `pi` and enter

`wget -O - https://raw.githubusercontent.com/monero-ecosystem/PiNode-XMR/master/Install-PiNode-XMR.sh | bash`

You will see the screenshot above to make your selection. Follow the on screen instructions.

It is a relatively fast process except for the compiling of Monero from source which is CPU and RAM intensive, % progress readouts are given periodically. It is installed in 2 stages. 

Stage 1 sets up the environment for user 'pinodexmr', security and network. Once this is completed a restart is required (automatic).

Stage 2 once rebooted. Log back in with user `pinodexmr` and password `PiNodeXMR` and the script will continue to install. No further interaction is required. However the process of compiling Monero from source is lengthy and resource intensive. For Pi 3b+ expect ~8hours for completion, for Pi 4 ~4hours.



### All other devices - Armbian Debian Buster OS


Install the official Armbian Debian Buster OS, minimal or lite if available for your device. Perform normal first login actions, usually user: `root` and password `1234`.

**Create user** `pinodexmr` with a password of your choice. (this is essential, all lower case, as shown to the left)

Then to install, whilst still logged in as root, simply enter:

`wget -O - https://raw.githubusercontent.com/monero-ecosystem/PiNode-XMR/master/Install-PiNode-XMR.sh | bash`

And make your `Armbian` selection.

It will perform it's security and network actions as root. Then it will ask you if your device requires a swap file. You will require one if your device has less than 2GB of RAM for the Monero compilation later.

The device will then reboot and require you to login as `pinodexmr`. Installation will resume automatically, which for this last stage takes several hours dependent on the power of device.

Once complete you'll be presented with the screen below, and your device will do it's final reboot. You can now proceed directly to the [Web-UI and password setup section of this page](https://github.com/monero-ecosystem/PiNode-XMR#setup) for an overview of how to navigate PiNode-XMR. Just ensure before starting your node you set a new RPC username and password from the web terminal menu, a local time-zone may also need setting.

Welcome to the PiNode-XMR community!

![PiNode-XMR landing page](https://github.com/monero-ecosystem/PiNode-XMR/blob/master/Screenshots/Install-Complete.png)

## Downloads
#### Download PiNode-XMR disk image for Raspberry Pi 3b+ & 4
If using a Raspberry Pi you may use the pre-installed disk image. The PiNode-XMR image is available to download as-is. Meaning it is un-compressed and ready to write using the same method you would for any other disk image. 

____
#### Direct Downloads

[Download PiNodeXMR v4.21.01 Base image for Raspberry Pi3B/4](https://drive.google.com/file/d/13CiIJ2TrZ5nxdwLto2OKcuowzq1v7-b5/view?usp=sharing) 7GB


Name: PiNodeXMR-v4.21.01.img

Size: 7088381952 bytes (6760 MiB)

SHA256: BE0531C90EAE4D3D768D10826AF09084270475CB78E77793CBA5D7B304C73C99

____

[Download PiNodeXMR v4.21.01 Pre-sync'd and Pruned disk image to block 2278908 for Raspberry Pi 3B/4](https://drive.google.com/file/d/15OnZMx8M0bsgUN4W6-h7mg9fWLsOUzVk/view?usp=sharing) 40GB

Name: PiNodeXMR-v4.21.01-prunedToBlock2278908.img

Size: 43458240512 bytes (40 GiB)

SHA256: 202FAA2BF71EC1A2914A216E48F95C2C3EB9F1C0677124AD37B516A276CFE2B2

____

#### Torrent downloads [magnet links]

[Download PiNodeXMR v4.21.01 Base image for Raspberry Pi3B/4] 2.3GB

```
magnet:?xt=urn:btih:bdfdf0ef3b94e4a8aa15dd2a0ed17aafb0243d74&dn=PiNodeXMR-v4.21.01.zip&tr=udp%3a%2f%2ftracker.opentrackr.org%3a1337%2fannounce

```

Name: PiNodeXMR-v4.21.01.zip

Size: 2437957944 bytes (2325 MiB)

SHA256: 74CC71A0202834E972678587E7B5875CDF383FD927B00A7419CB355F2DE55252

*Note, this is the hash for the zipped/compressed file. Once extracted the image can be verified with the direct download .img hash if you choose to. Torrent files kindly provided by JackieCat.

____

[Download PiNodeXMR v4.21.01 Pre-sync'd and Pruned disk image to block 2278908 for Raspberry Pi 3B/4] 28.2GB

```
[magnet:?xt=urn:btih:494ca720db6053f892393aebc9c9129a1323def4&dn=PiNodeXMR-v4.21.01-prunedToBlock2278908.zip&tr=udp%3a%2f%2f9.rarbg.to%3a2710%2fannounce&tr=udp%3a%2f%2f9.rarbg.me%3a2710%2fannounce&tr=udp%3a%2f%2ftracker.opentrackr.org%3a1337%2fannounce&tr=udp%3a%2f%2ftracker.internetwarriors.net%3a1337%2fannounce&tr=udp%3a%2f%2ftracker.cyberia.is%3a6969%2fannounce&tr=udp%3a%2f%2fexodus.desync.com%3a6969%2fannounce&tr=udp%3a%2f%2f3rt.tace.ru%3a60889%2fannounce&tr=http%3a%2f%2f5rt.tace.ru%3a60889%2fannounce&tr=udp%3a%2f%2fexplodie.org%3a6969%2fannounce&tr=udp%3a%2f%2fp4p.arenabg.ch%3a1337%2fannounce&tr=http%3a%2f%2fp4p.arenabg.com%3a1337%2fannounce&tr=udp%3a%2f%2ftracker2.itzmx.com%3a6961%2fannounce&tr=udp%3a%2f%2f47.ip-51-68-199.eu%3a6969%2fannounce&tr=http%3a%2f%2fopen.acgnxtracker.com%3a80%2fannounce&tr=udp%3a%2f%2fwww.torrent.eu.org%3a451%2fannounce&tr=udp%3a%2f%2ftracker.torrent.eu.org%3a451%2fannounce&tr=udp%3a%2f%2ftracker.tiny-vps.com%3a6969%2fannounce&tr=udp%3a%2f%2ftracker.ds.is%3a6969%2fannounce&tr=udp%3a%2f%2fopen.stealth.si%3a80%2fannounce&tr=http%3a%2f%2fopentracker.i2p.rocks]

```

Name: PiNodeXMR-v4.21.01-prunedToBlock2278908.zip

Size: 30350869562 bytes

SHA256: EEA83A2D15BA0B65267999D514821E7F67622D3003F3FC69C428057625E4376B


*Note, this is the hash for the zipped/compressed file. Once extracted the image can be verified with the direct download .img hash if you choose to. Torrent files kindly provided by JackieCat.

____

For those that are new to writing Raspberry Pi image files these free programs will get you started:

1. Format the micro-sd card. For all users I recommend [SDFormatter](https://www.sdcard.org/downloads/formatter/)
2. Write the image file to the formatted card. 
   - Windows users [Win32DiskImager](https://sourceforge.net/projects/win32diskimager/)
   - Mac users [Etcher](https://etcher.io/)

Once complete insert the card into your device and power on.

## Setup:


On first time power-on the software will check to see if it has booted before. On it's first usage it will resize it's rootfs partition automatically to make best use of whichever size MicroSD card you've purchased ready for the Monero Blockchain.

During this process it will restart itself and will pause for 120 seconds. This is normal. I recommend that once plugged in simply leave the node for 5 mins, after this time it will have self configured and you will be safe to continue setting your passwords (covered in a bit).

Every subsequent power-on event will skip this step and immediately run the Monero software without delay in the condition it was last run in, Clearnet/tor/Mining. Pruned or not.

Your Web-UI should be available on pinodexmr.local from your browsers address bar. If not it may be required to enter the IP address of the Node into the web browser of a device . If you don't know how to find the IP address you can [read about some methods on the Raspberry Pi doc library.](https://www.raspberrypi.org/documentation/remote-access/ip-address.md) 

When you enter this IP address into the web browser of a device on the same network as your Node you'll be presented with the following screen...


![PiNode-XMR landing page](https://github.com/monero-ecosystem/PiNode-XMR/blob/master/Screenshots/index.png)

From here click on "Web Terminal" from the top navigation bar. You will most probably get a warning that it isn't a secure site. I haven't yet configured SSL certificates yet so this is normal. Click proceed and login with the default Username and password of:

Username: pinodexmr

Password: PiNodeXMR

*Note: Armbian users may have already set a different password*

![PiNode-XMR web terminal](https://github.com/monero-ecosystem/PiNode-XMR/blob/master/Screenshots/Welcome_screen.png)

If this is your devices first boot then follow the select "System Settings" and the two password setting options should be used for "Master" and "RPC". 

Once the passwords are set the device is yours. Head back to the Web UI to start your node.

## Web-UI: Starting your Node and General Usage

### Welcome page -
I won't duplicate the homepage screenshot used above as there's not a lot to say about it apart from the PiNode-XMR version number (presented version#.YY.MM). However a shout out to the guys at https://designmodo.com/ for the template of the Web-UI. Their template has made this build much quicker. Check out their site if you're ever in the need of an interface for a project.

I'll also take this opportunity to mention that most of the displays of Node and Hardware data within all the UI are updated every 60 seconds (with the exception of the 'storage usage' section on the 'Node Status' page which updates every 4 hours), so in most cases hammering the refresh button won't provide new data until it is sourced and processed in the background.

## Advanced Settings - Starting Monero

This is the main page for starting/stopping and setting variables on your node. It can either be started as a Clearnet Private/Public,tor or Mining node, and you may switch between modes as you wish. The node has memory, so if power is lost and restored the node will reboot and continue in the mode it was last set, hence the wording on the Node Status page to remind you what you last clicked.

### Clearnet Nodes
![Clearnet Nodes](Screenshots/clearnet.png)

These nodes will broadcast all transactions over IPv4.

- *Private Node:* A node that only you can connect a wallet to using the RPC username and password you've set. How you configure your firewall will determine external access, (covered later)

- *Public Node (Free External RPC):* A full public node that is free to all users anywhere in the world. You can set a custom port here if you want, but whatever port is used must be [forwarded.](https://github.com/monero-ecosystem/PiNode-XMR#port-forwarding)

- *Public Node (Requires RPC Pay):* Be a little patient for this cool new feature, where you could be paid to run this node. See [Monero project commit message for this feature](https://github.com/monero-project/monero/commit/2899379791b7542e4eb920b5d9d58cf232806937). This feature is installed but waiting for a fix to be committed. More info on the issue [monero-project pull #6260](https://github.com/monero-project/monero/pull/6260) & context [monero-project issue #3083](https://github.com/monero-project/monero/issues/3083). Expect to be active on release of Monero 0.15.0.3. I've put the settings is according to this documentation but have been unable to test yet. Minor tweak at time of release may also be necessary.

**To switch from one mode type to another use the appropriate stop button for the service that is running. To indicate which version is running your node will tell you on the “node status” page.
Stop the current service before starting a new one.**

### Mining

![Mining](Screenshots/mining.png)

TBH this is a feature I expected people to ask for and it was simple enough to implement so it's included. The Raspberry Pi is absolutely unsuitable for this purpose, but there it is. 
Enter your address on the right and the page will confirm submission with a read-back. Hit start (once all previous instances of the node have been stopped) and enjoy your sub 1H/s. Setting mining intensity (default 50%) can  be found in the build/developer notes at the end of this manual.
A final note on this, now I've updated to v2 of this project and RandomX has come along mining is even less suitable in a Pi. However I intend to step away from making disk images and instead produce installing scripts so this software can be installed on devices other than Pis. Then this feature may once again have a use.

### Anonymity Nodes

![Annonymity Nodes](Screenshots/anonymity.png)

Run a private node that broadcasts your transactions over either Tor or I2P.

**To use either of these modes you must first install the relevant option via the [web terminal](#extra-network-tools)**

- *TOR:* When you choose to install tor PiNode-XMR generates a unique tor onion hostname to you for your hidden service. It is displayed here as "Public Address". The one trick here is that you need to add a seed node for your first hop to the network. To quote the [official documentation](https://monerodocs.org/infrastructure/tor-onion-p2p-seed-nodes/):
 >Your monero daemon will discover other P2P nodes but it needs to start somewhere. These starting nodes are known as "seed nodes". For clearnet the seed nodes are hardcoded in the software so no configuration is needed.
 
 ### Global Settings

![Global Settings](Screenshots/global_settings.png)

- *RPC Port:* Here you can set the *unrestricted* RPC port.

- *Bandwidth:* Here are some drop-down boxes for you to interact with if you think the node is hogging too much of your network bandwidth. If you select a value from the list the new variable is  considered “pending”. It takes a node stop+start for changes to take effect.

- *Swap File:* If your device has less than 2GB of RAM then you'll probably need to turn on the swapfile when building monero.

- *Shutdown:* To gently shutdown+power off the node use the stop buttons as  normal and then hit this “shutdown” button. It will complete it's shutdown process in 60 seconds.

- *Kill:* (Not power off) Try not to use this, but it's there. I guess it's in case you cant remember what mode your node is in and the “status” page isn't helping. Ideally use each stop button in turn for a safe shutdown then maybe you could hit this to be sure? Dunno, this'll probably disappear in a future release.

## Node Status -

![Node Status](https://github.com/monero-ecosystem/PiNode-XMR/blob/master/Screenshots/nodestatus.png)

This is the go-to page for the overall health of the node showing summaries for the Monero software and you'll also find hardware info such as RAM usage, CPU temperature and storage usage. At the bottom of this page you'll also find a toggle button to enable/disable the 2GB swap file. This 2GB swap file is designed for use when asking the node to perform intensive tasks such as the initial sync, pruning or if you were to ever import a new blockchain from an external device. Under normal operation of the node once sync'd it is advised to disable the swapfile to preserve the read/write health of your storage device.

## Monero Blockchain Explorer

![Block Explorer Status](https://github.com/monero-ecosystem/PiNode-XMR/blob/master/Screenshots/blockexplorer.png)

**New** With some collaboration from its maker reddit user /u/mWo12 I've managed to include his "Onion Monero-Blockchain Explorer" which is a fantastic tool for any auditing needs you have and don't want to send view_keys to any external website/untrusted source. It also includes a transaction pusher for those cold wallet users. The Explorer is all open source and can be found here [Github - Onion Monero Blockchain Explorer](https://github.com/moneroexamples/onion-monero-blockchain-explorer). Many thanks to /u/mWo12.

## Transaction Status

![Transaction Status](https://github.com/monero-ecosystem/PiNode-XMR/blob/master/Screenshots/transactions.png)

A very useful page. Here you can check to see if a transaction you have broadcast has done so successfully. Most web browsers have a search function (CTRL+F) use this to search the page by Transaction ID and if broadcast it will find it in the lower box.

The Overview above gives a picture of the general network condition and estimates (if there is a backlog) how long it will take to clear with full blocks.

## Connection Status

![Connection Status](https://github.com/monero-ecosystem/PiNode-XMR/blob/master/Screenshots/connectionstatus.png)

Displays OUT and IN peers along with their 'state' which is commonly either 'normal' or 'synchronising' it also gives some detail to data consumption.

The White/Grey list are nodes that are recently active/silent respectively. A healthy node should have plenty of 'white' nodes but the list ca take some time to grow.

That list of nodes is viewable in full at the bottom of the page.

## Log:

![Log](https://github.com/monero-ecosystem/PiNode-XMR/blob/master/Screenshots/logs.png)

A 5 MB rolling log is kept here. Should you suspect your node is not performing as it should you may find a clue as to why here. I strongly suggest that if you find [WARN] flags here that you consult google first. Monero is plenty developed by now that most questions have been answered by other users, and most warnings (once investigated of course) can be safely ignored and are connection related as peers drop off the network.

## Web-Terminal: & Main System Menu

## System Settings

![System-Settings](https://github.com/monero-ecosystem/PiNode-XMR/blob/master/Screenshots/system-settings.png)

### Raspi-config - Hardware management
 Here are the standard hardware config options that the Raspbian OS provides. A detailed explanation of each feature is best found at the official Raspbery Pi pages: https://www.raspberrypi.org/documentation/configuration/

However - some special notes on Wifi and the PiNode-XMR

- *WiFi:* One of the most asked for features is wifi. This can easily be configured at a beginner level and allows setting Wi-Fi SSID and password under 'network options' settings. Once configured the device will ask to reboot.

**However if Wi-Fi is to be used then the Ethernet cable must be unplugged. If you do not, the device will assign itself 2 IP addresses, one for each connection method, and Monerod will fail to boot**

### Master Login Password

This menu allows you to set a new root/pinodexmr user password. Doing so is strongly recommended to change from the default password.

When creating this password the input box cannot be empty, the password must be longer than 8 characters, alphanumeric aBc123, **no** special characters %^-_

This password will be used to log into the web terminal in future and for those that access via SSH. If you forget this password you will be locked out of these menus, keep it safe.

### Monero RPC Password and username

This menu allows you to set a new root/pinodexmr user password. Doing so is strongly recommended to change from the default password.

When creating this password the input box cannot be empty, the password must be longer than 8 characters, alphanumeric aBc123, **no** special characters %^-_

This password/username combo is used to connect your wallet to this node.

### USB storage setup

For storage the ideal configuration is to have your OS and PiNode-XMR on your standard media that your device supports, then have the monero blockchain separately on a USB SSD. This has been proven to have faster sync times.

However this menu option will allow you to store the blockchain on any USB device over 100GB. It will run several checks, and on your command format (wipe) the drive and mount it for use with the PiNode-XMR. It also labels the drive "XMRBLOCKCHAIN" and can be re-detected by PiNode-XMR future installs so should the worst happen and your SD card fail, on installing a new PiNode-XMR it should detect the configured drive and continue.

*Notes on USB storage - *

The entire drive will be used for PiNode-XMR, this helper doesn't have the facility for multiple partitions. You are welcome to make your own partitions from the command line, just be sure to mount the blockchain partition to ~/.bitmonero, and if you want to auto-mount of boot, add the UUID of the partition to /etc/fstab

As of PiNode-XMR V3.##.## a new filesystem format is used which greatly improves compatability accross operating systems. This has been made possobile thanks to JElchison and the [format-udf project](https://github.com/JElchison/format-udf).
The new script will still detect the legacy ext4 filesystems from previous versions however the newer system is now UDF. This has the advantage of being detected accross all major OS's. This allows you to copy your blockchain onto this configured USB device from another source, PiNodeXMR will then detect and use it. JElchison's project creates a fake MBR on your device which is self contained within sd#1 partition itself. Very clever, and meets requirements of both Microsoft and Apple systems.

To import a blockchain simply add the a whole LMDB diretory to the top level of the device. Ensure you trust the blockchain's source.

### Agnostics - SD card health checker
A new tool for checking SD card read/write sequential and random speeds. It has some performance targets set into it and will inform you whether or not you meet those targets via PASS/FAIL.

Before starting this test ensure you have stopped the node and block explorer, if they read/write in the background the test will fail.

## Update Tools

![Update-Tools](https://github.com/monero-ecosystem/PiNode-XMR/blob/master/Screenshots/update-tools.png)

### Update Monero
PiNode-XMR will download a new version number from this site and compare it to your current version. If the new version number is higher you will have the option to update.
On update the nodes and block explorer will stop, old Monero versions deleted and new versions will be downloaded and built from the official Monero repositories.

The compiling of Monero on single board computers is very CPU intensive, at worst on a Raspberry Pi 3b+ it has been known to take approx 7 hours. More powerful hardware will be proportionately faster.

### Update PiNode-XMR
This will update your Web UI, install new tools, features that are not covered by another option in this Update menu.
If you have set custom variables during normal use (Bandwidth settings, Addresses, passwords) they will be retained during the update process.

### Update Block-Explorer
As the title suggests. If there is a new version available it will be sourced from the external repository https://github.com/moneroexamples/onion-monero-blockchain-explorer

### Update background system dependencies
This option runs the command `sudo apt-get update && sudo apt-get upgrade -y` to update background dependencies that are used by the underlying operating system (Raspbian or Armbian). This can include things like security upgrades so is worth running on occasion.

## Node Tools

![Node-Tools](https://github.com/monero-ecosystem/PiNode-XMR/blob/master/Screenshots/node-tools.png)

### Start/Stop Blockchain Explorer
As the title says, use this to manually start/stop the explorer.

When the explorer is started it also updates a flag elsewhere in the system so that the explorer will be re-started on system boot (in case of power cycle). This flag is then removed on the manual stop selection.

For full features see the [onion-monero-blockchain-explorer github](https://github.com/moneroexamples/onion-monero-blockchain-explorer#onion-monero-blockchain-explorer-features)

The emission monitor is enabled and has been limited to 1 CPU thread. When started, the thread will initially scan the entire blockchain, and calculate the cumulative emission based on each block. This is can be a time consuming heavy read/write process. It is advised to wait until your node has 100% sync'd before starting the block explorer.


### Prune Node
I think this is the simplest method for new users. By using the command this way the pruning binary will display it's progress and once complete will edit all start commands to use the pruning feature on future starts. For this reason the prune option can only be used once, and the node doesn't currently have a script to reverse the process. Once you have signalled your node to be a pruned node it is fixed as such. I will include instructions at a later date for how to revert back to full-node.

### Pop Blocks
Another new feature. This uses a blockchain tool stored on your system to remove a specified number of blocks from the end of the blockchain. It will prompt you for a value, and that many blocks will be removed.

Ensure the blockchain is not in use by the node or explorer first, (stop them).

This can be used is you have blockchain transaction errors preventing you from completing a sync. It can help avoid a lengthy re-start sync from scratch.

## Extra Network Tools

![Network-Tools](https://github.com/monero-ecosystem/PiNode-XMR/blob/master/Screenshots/network-tools.png)

## Install tor
From v3 of PiNode-XMR tor is no longer installed by default due the potential for a user to encounter trouble from censorship, political or legal issues in their country. Therefore use this option to add the tool and enable the tor mode on the web UI. Once installed see https://github.com/shermand100/pinode-xmr#tor below for how it works, and how it affects your privacy.

## tor NYX
Is a bandwidth monitoring utility for tor, (Previously tor-arm).

Detailed bandwidth stats are available when running as a tor node using the nyx utility. (Available for Raspberry Pi image only) It is installed as a package with the "Install tor" option mentioned above. 

Selecting tor NYX will bring you to the terminal and be prompted for the controller password, use: `PiNodeXMR`

![tor-ARM screenshot](https://github.com/monero-ecosystem/PiNode-XMR/blob/master/Screenshots/arm.png)

Exit the utility by using `CTRL+C` and return to the setting menu.

## Install PiVPN
This is a great open source tool from https://www.pivpn.io/ enabling you to run your own home VPN. Check out their site for more info

## NoIp.com Dynamic DNS
This can be helpful if you have a dynamic external IP address, and want to connect to your Node from a mobile wallet on the go. This service lets you set a easy to remember hostname which will always point to your home network. Port forwarding is then required to complete the connection to your PiNode-XMR, and concern should be given to your home security settings before allowing this. Configured correctly this is a great tool.
Before starting this option it is required that you register (free) at NoIP.com for a username and password that will be required after installation. From their site you set your custom hostname.

## tor
A note on tor:
Your PiNode-XMR utilises tor in Monero's default manner. To quote https://github.com/monero-project/monero#using-tor :

> ' The feature allows connecting over IPv4 and Tor simultaneously - IPv4 is used for relaying blocks and relaying transactions received by peers whereas Tor is used solely for relaying transactions received over local RPC. This provides privacy and better protection against surrounding node (sybil) attacks. '

and https://github.com/monero-project/monero/blob/master/ANONYMITY_NETWORKS.md#behavior :

> ' If any anonymity network is enabled, transactions being broadcast that lack a valid "context" (i.e. the transaction did not come from a p2p connection), will only be sent to peers on anonymity networks. If an anonymity network is enabled but no peers over an anonymity network are available, an error is logged and the transaction is kept for future broadcasting over an anonymity network. The transaction will not be broadcast unless an anonymity connection is made or until monerod is shutdown and restarted with only public connections enabled. '

## Misc options:
### *Mining_Intensity:* The default mining intensity is set to 50% and is configurable through the web terminal command line

     nano /home/pinodexmr/mining-intensity.sh

 Where the value '50' can be between 0-100. Save changes with > ctrl+O exit the editor with > ctrl+x.
 Monerod will require a restart for mining intensity changes to take effect. Carefully monitor your CPU temp, the Pi will auto-throttle CPU voltage at ~82'C


## Connecting a Wallet - LAN
### Monero GUI
To use your Monero GUI on a device that is on the same local network as your node enter the IP address you have been using to view the interface into the remote node page of the GUI, port 18081 and the RPC username/password you set in the ./setup.sh menu. You may also select ' mark as trusted daemon ' as it's your trusted node.

![GUI-screenshot](https://github.com/monero-ecosystem/PiNode-XMR/blob/master/Screenshots/GUIremote.png)

Your wallet will then scan the node's blockchain for any transaction outputs that belong to your wallet, this can take a few minutes the first time but subsequent connections will only scan for changes since the last connection being much faster.

### Monerujo app
Unfortunately the app won't allow a screenshot, but it's very similar to the GUI method.
With your mobile device connected by WiFi to the same network as your node simply enter the node IP in the 'hostname' field, port is 18081. 'Node name' is for your reference on your apps node list, call it what you want. Username and Password are required and are the RPC username and password you set in the ./setup.sh menu.

## Connecting a Wallet - External Connections

### IP address considerations

*Some background on this section...*

Most users of a PiNode-XMR node will be doing so from their domestic internet connection rather than through the internet connection of a large corporation. In almost all cases IP addresses are leased to you by your domestic internet provider, and that lease typically expires after a few days. When the lease expires on your IP address you may be given a new address or you may be re-assigned the same number for a few more days. This would happen without your knowledge and is completely normal.
Where this causes a problem for us is that we're reading this chapter with the view to connect our mobile wallet for example to our PiNode-XMR at home so we can spend our funds whilst on the go and out of range of our home WiFi. However if whilst we're "on the go" our home IP address were to change because what is called the DHCP lease expired we would not know our new IP address that was assigned to us and connection wouldn't be possible. So we have some options and everyone's situation will be different:

* Just hope it doesn't change
  * As simple as it sounds it really may not change for several months, you could keep getting leased the same IP but every service provider policy is different. Some users have been known to be re-leased the same IP over and over and others change frequently between addresses assigned to your area. You never know. You could get lucky.
* Ask your Internet Provider for a static IP.
  * Providers may be able to offer what's known as a static IP - one that doesn't expire. These however can come with a fee or are only available on their top tier packages. You get the idea but it can't hurt to ask.
* Dynamic DNS
  * This is a solution that is included with your PiNode-XMR if you wish to download and enable it. It can be found at the end of the ./setup.sh process.  The idea behind this is that you make an account with a Dynamic DNS provider, in this case noip.com. The company noip.com instead of giving you an IP address let you choose a hostname (for example I chose whilst trialling was pinodexmr.hopto.org). This can also be easier to remember. A small program runs on the PiNode-XMR that monitors it's public IP address and if a change is detected it notifies noip.com of the new IP address. Noip.com then updates it's index so when I request my wallet connection to pinodexmr.hopto.org noip.com refers the traffic to whatever my new public IP address is from it's index and I never have a problem with my dynamic IP address. It's worth mentioning that your internet traffic is not routed through them, they are what's known as a DNS server, the same as when you type www.bbc.co.uk a DNS server turns those words into an IP address and you are referred to your destination. Like an address book for the internet pointing traffic to it's destination.

 *There are lots of online services that provide Dynamic DNS and I plan to add more so you as a user have more choice. I've no affiliation with noip.com. I just chose them because they're free and have a simple linux installer. I should also mention their software is not installed on the PiNode-XMR by default, it is only downloaded if selected from the ./setup.sh script*

* VPN
  * Using a VPN you may be able to connect your mobile device to your home network so your wallet connects as though you are still at home. I have not used this method, but it may be the preferable method for privacy as all traffic from the wallet to the node would be encrypted, masking that you are even using Monero at all. {Community input?}

### Port forwarding

So once you've got an IP address that consistently points to the network the PiNode-XMR is in we're ready for the last step, port forwarding.

The IP address or hostname if you use Dynamic DNS points to your router. If you open your router settings you should see some options for port forwarding. The idea here is that you are going to tell the router that any external traffic it receives on a specifc port (usually 18081 or 18089 for Monero RPC) should be directed to the PiNode-XMR IP (usually 192.168.xx.xxx) and that same port.

Depending on which mode you started the node in above you will want to open different ports (assuming you didn't change the defualt port values):

* Prive Node: Forward port **18081**
* Public Node (Free External RPC): Forward port **18089**
* Public Node (Requires RPC Pay): Forward port **18083**

Additionally, you may want to also forward port **18080** to help other nodes sync their blockchains.

Every router has a different configuration menu so you may have to refer to it's manual if you're unsure. Alternatively there are some nice examples for multiple brands here with pictures.

https://www.noip.com/support/knowledgebase/general-port-forwarding-guide/

(I know noip.com again :) but they refer to how to check if your port is open using the hostname which may be of use if users take the Dynamic DNS route)

This then opens an internet connection to the outside world, it is therefore essential you have changed your password from the default to something long and un-guessable. I've also installed a program called fail2ban which should offer some additional protection. If an external user makes 3 unsuccessful login attempts within 10 minutes, their IP address is banned for 10 minutes. This helps mitigate against brute force attacks.

You can now connect your mobile wallet to your PiNode-XMR from anywhere in the world! Using your static IP or DNS hostname, port 18081 and the RPC username and password you set in ./setup.sh
