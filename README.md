# Homelab-Network-Infrastructure
My Home Network Setup!


How it began: 
1. I noticed a major dead zone next to my PC. I ran a speed test and noticed I was around 40 megabytes per second (mbps) for download, and a little under for upload. (A general rule of thumb is your download should be around 6-10 times your upload speed, meaning a lot of the data was being slowed down by the structure of my house.)
2. I was having another issue where I couldn't login to my laptop running my proxmox hypervisor for my game servers. If I took down a server for maintanence and wanted to boot it back up remotely, the only way I knew how was to open a port to the internet. Pretty terrible idea.
3. Speaking of opening up a port to the internet, I want my friends to be able to connect to my game server securely. The problem is, it takes a lot of setup for a game you may play for a couple of hours and then never again, so it wasn't worth it to have a complex setup.



I started learning a bit about how stuff worked. My first solution was just to try to run my Xfinity Gateway (a single brick for my modem, my router, and the singular access point of my house) and connect this to a Firewalla Gold SE. This failed miserably as the Firewalla model I was using wasn't able to be configured as an access point, and I actually got locked out after setting my modem to bridge mode. Pretty miserable ngl as I had to factory reset my families internet.

I watched a few videos on how networking devices had to be configured and how I could properly set my home up for success, and so began the plan:

1. A network needs to be supplied via an ISP. It travels through the modem, from a WAN port, plugged into a WAN port on a firewalla. This sends the data straight through to an access point. If you want to get fancy or are in a work environment, you would first send this through a switch device and then to your access points. In order to create my mesh network, I had to actually do this so that all the access points were first on the same network. After that, you can put separate access point devices across your house and ensure a super stable environment.

2. Where I was unable to connect to my game server unless I was on my home network, I set up a WireGuard VPN. This allowed my singular laptop to securely access my home network once I enabled it, ensuring a smooth and encrypted experience. I could now boot up game servers, mess with my NAS 4800dxp from ANYWHERE in the world.

3. The last thing I needed was a bit more difficult. I realized I couldn't really do much else other than opening a port up to the internet which sucks. Obviously you set up firewalls and do what you can, but if your device is on the internet it is hackable with no way around it. To try and help a bit, I set up a ufw (uncomplicated firewall) for on every Ubuntu Linux VM I ran within proxmox. I set up SSH key based authentication so only a few devices with proper keys could access. I used least privilege principle on my IAM users for my AWS S3 backups, but I always kind of just had a weird itch about it as I didn't really like it. Kind of like I was on my toes waiting for the notifications or a log to state it was over and my network was fried. If only my laptop could be on a completely different network: 

Virtual Local Area Networks (VLANS) are basically a divide between one part of your internet and another. This isolates specific devices and if one of my game servers did end up getting hacked, it doesnt affect the rest of my network.
After setting this up, I felt much more secure. If I managed to lose a massive fleet of VMs within that laptop at any given time, my family was safe from any threats. I had isolated the opening to a small, specific part of my network.


This project was an awesome learning experience. From frustration to a secure, high-performance home lab. By addressing a series of real-world problems: poor Wi-Fi performance, a lack of secure remote access, and network security concerns, I've built a much more robust and reliable network infrastructure. This setup not only delivers great speeds but also gives me the control and peace of mind neccesary to continue developing.
