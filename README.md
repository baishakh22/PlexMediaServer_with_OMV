# PlexMediaServer_with_raspberryPi
Create a Plex Media Server using OpenMediaVault. But the big question is what is the open media vault?

OpenMediaVault (OMV) is a free and open-source network-attached storage (NAS) software solution. It is designed to turn a regular computer or network-attached storage device into a powerful and user-friendly file server and media server. OMV is built on top of the Debian operating system and provides a web-based graphical user interface (GUI) for easy management and configuration.

To start the process there are three (3) major steps that need to follow.

  1. Setup Raspberry Pi
  2. Configure OpenMediaVault.
  3. Add Network Location


## Raspberry Pi Setup

To set up the Raspberry Pi, we need an Imager/Burner tool. As we are using Raspberry PI, they already have an Imager tool, called ```Raspberry Pi Imager```. For this project, I used a 128 GB SD Card. Now follow the steps:
  1. Plug in the SD Card to my PC
  2. Open the Rasberry Pi imager.
  3. For Operating system Choose, Raspberry Pi OS (other) > Raspberry PI OS Lite (32-bit) [^1]

[^1]: This is command line OS. 

![Screenshot 2023-09-13 at 7 43 54 PM](https://github.com/baishakh22/PlexMediaServer_with_OMV/assets/93491482/94843414-4fe9-4ee2-bce5-1e10f40b7784)

![Screenshot 2023-09-13 at 7 44 00 PM](https://github.com/baishakh22/PlexMediaServer_with_OMV/assets/93491482/2b2ec5bc-2ae4-4903-a3e3-93b93c0f2db0)

  4. Select your SD  card for the Storage.
  5. Now, before hitting write, make sure your ```SSH Setting is turned on```.
  6. To enable SSH, press ```Ctrl + Shift + X ```, make sure, you "Enable SSH", and set up username and password. Image customization options should be "to always use". 

![Screenshot 2023-09-13 at 7 48 45 PM](https://github.com/baishakh22/PlexMediaServer_with_OMV/assets/93491482/e3d1201f-fc2d-4dd0-a5c3-e976afd5be80)

  7. After configuring this, it's time for "Write"

This might take a little bit of time. After brun the SD Card it will automatically eject the SC Card from your pc. You can remove the SD card and plug into the Raspberry Pi.

  8. After plugging in the SD card to the Raspberry Pi, turn on the power button.

This will take a little bit of time to boot up the process. I have the patience to wait, I want to see what is actually going on in my Raspberry Pi, so I connect my monitor to it, and see how they boot up.



## Find the IP and Connect with SSH
Now after you respberry pi boot up, it has an IP address that is assigned from your router. You can find this IP from your router settings. I didn't find it. So I used ```AngerIP``` tool to find my IP address. It gave an IP address (192.168.x.x). With this IP address I follow the procedures

  1. Connect with my Raspberry Pi with my ```cmd```, by following command:

     ```
     ssh ip@192.168.x.x
     ```
  2. Update my Pi,

     ```
     sudo apt update && sudo apt upgrade
     ```



## Install Open Media Vault
After updating my IP, I installed the open media vault by running the following command:

```
wget -O - https://raw.githubusercontent.com/OpenMediaVault-Plugin-Developers/installScript/master/install | sudo bash
```

This process takes a long time. Probably 10-15 mins. Then when it finished, we installed OMV on my Raspberry Pi. 

Now follow the steps:
  1. Open up a browser and type your Pi's IP. Sometimes, in the installation process of openmediavault, your IP might change. So make sure which IP is currently used by your Pi. 

```
192.168.x.x
```

![Screenshot 2023-09-13 at 8 09 51 PM](https://github.com/baishakh22/PlexMediaServer_with_OMV/assets/93491482/bbff7710-d697-44f0-9eb8-c9ab8029d2e8)

In this login area type the default username and password

```
username: ADMIN
Password: openmediavault
```

  2. After login to the system, Connect your external drive. Make sure it is connected. To check go to "Storage > Disks"
  3. ```Wipe``` everything on this hard drive. To wipe hhd/ssd click Storage > Disks. Select your hard drive and click wipe.  

![Screenshot 2023-09-13 at 8 28 39 PM](https://github.com/baishakh22/PlexMediaServer_with_OMV/assets/93491482/78f73e69-1dce-4a6f-888d-cb0054fe3331)

  4. Mount a File System

To mount my hard drive, I click Storage > File System > +. Top left corner there is a plus sign (+), click there and select ```ext4```. Then Select the drive.

![Screenshot 2023-09-13 at 9 14 09 PM](https://github.com/baishakh22/PlexMediaServer_with_OMV/assets/93491482/ebe88ce6-4888-446f-8bfb-5f97758fb8d4)
![Screenshot 2023-09-13 at 9 16 26 PM](https://github.com/baishakh22/PlexMediaServer_with_OMV/assets/93491482/d42ed438-7f77-496b-9ef1-8ee37ebac065)

  5. Click "Apply Change" on the top. 
  6. Create a shared folder.
Shared folders help organize your data in a structured and logical manner. By categorizing and segregating files into different folders, it becomes easier to find and manage specific files or types of data.

https://github.com/baishakh22/PlexMediaServer_with_OMV/assets/93491482/d73f334d-05f7-4ffe-b0ca-b34736e4ca30

  7. Permission on Share Folder.

https://github.com/baishakh22/PlexMediaServer_with_OMV/assets/93491482/70dd7c9d-b69f-49e7-9f31-2aabe286a07a

  8. Enable SMB services. Then share the services. 

Enable SMB Services:

https://github.com/baishakh22/PlexMediaServer_with_OMV/assets/93491482/57529601-5af7-43d5-900f-539aa663faf7

Share SMB:

https://github.com/baishakh22/PlexMediaServer_with_OMV/assets/93491482/32212d42-9117-43b4-a9b9-0448cc975b99

  9. Do the same process for NFS services. 

https://github.com/baishakh22/PlexMediaServer_with_OMV/assets/93491482/ef725ec7-b5b2-4919-99ef-f0e6f77ef98d

  10. Change the Password for openmediavault access for the admin.

https://github.com/baishakh22/PlexMediaServer_with_OMV/assets/93491482/e14f406d-7d84-419e-a8bc-075208177b74


## Create a Network Drive on your windows. 

https://github.com/baishakh22/PlexMediaServer_with_OMV/assets/93491482/196ae836-28ba-4741-98ff-8674735da67d

## Install Plex Media Server
  1. To install the HTTPs transport package, we create an SSH Connection to Pi again and type the following command:

```
sudo apt-get install apt-transport-https
```


  2. Add the Plex repositories by typing the following two(2) commands. Don't type run those two commands at the same time. 

```
curl https://downloads.plex.tv/plex-keys/PlexSign.key | sudo apt-key add -
```

```
echo deb https://downloads.plex.tv/repo/deb public main | sudo tee /etc/apt/sources.list.d/plexmediaserver.list
```

  3. Update the PI again

```
sudo apt-get update
```

  4. Install Plex

```
sudo apt install plexmediaserver
```
