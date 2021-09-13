# RPI-Plex-Media-Server-with-external-HDD
Guide to set-up your RPI Plex Media Server with an external HDD

I spent some time trying to set up my PMS (Plex Media Server) on the RPI4 (Raspberry Pi 4) and struggled to find all information in one place so I thought I will put all the information in one place.

If you are reading this you probably already have Raspbian running on your RPI. Otherwise, go to https://www.raspberrypi.org/software/, get the imager tool and download the latest Raspbian onto your chosen MicroSD card. Once done you can either SSH into it or set up VNC so you can easily remote into it for GUI.


USING SSH:

If you want to use SSH, before booting you will have to create an empty ssh file without any extensions on the boot partition of your microSD card where you have installed the image using the raspberry imager tool. This will allow you to use it as a headless device over LAN at least.
Feel free to set up WiFi setting too in the following doc if you do not want to use Ethernet connection.
See this page for more detailed docs: https://hackernoon.com/raspberry-pi-headless-install-462ccabd75d0.

USING VNC: 

I am using both SSH and VNC for different things I am trying to achieve. If headless, you will have to SSH into your RPI and type in:
sudo raspi-config
Then go into the interfacing options and enable VNC over there. 
See this page STEP 9 and 10 for more detailed docs: https://desertbot.io/blog/headless-raspberry-pi-4-remote-desktop-vnc-setup

INSTALl Plex Media Server on RPI:

You will have to install PMS from their repository. Feel free to ignore the Setting a Static IP Address for your Plex Server step for now.
See this page for more detailed docs: https://pimylifeup.com/raspberry-pi-plex-server/

ALLOWING PMS READ FROM EXTERNAL HDD:

This is what gave me the most headache and made me write this article in the first place.

Once you set up your VNC/SSH and PMS you will have to make sure that PMS can at least read the files of the given external HDD. 

I am using the ext4 journaling file system for my HDD. You can format that over your Windows or macOS machine. 
Or you can follow this article to get it done on your RPI: https://www.pidramble.com/wiki/benchmarks/external-usb-drives

Once your drive is ready to be used by PMS you will have to give the right permissions to the Plex server user that is created when installing PMS on your RPI.

Open your terminal and type in these commands:


sudo usermod -a -G pi plex

sudo usermod -a -G plugdev plex

sudo chmod 775 /media/pi


Once done PMS will be able to see files on your external USB connected HDD and display them in your PMS library.

Happy days!
