# How to Setup the Pi OS from scratch

* Install Tailscale
  * Easy follow guide on website
* Install python3
  * sudo apt-get update
  * sudo apt-get install python3.13
* Install docker and setup necessary containers
  * Must setup kuksa.val container and influxdb container
    * Steps will go here when I figure them out
* Connect ssh to GitHub account MAY NOT BE NECESSARY
  * ssh-keygen -t ed25519 -C "gmab222@uky.edu"  or your email in place of mine
  * Also might not be necessary if we make a “folder of stuff configured to send to the dashboard”
* Upload kuksa-can-provider with logs
  * I’m thinking about putting these both into the same directory
* Upload config stuff for kuksa.val
  * It's important to upload because you wont get the config right doing it yourself just like the previous time you did this.
* Install Flutter using Snap
  * https://snapcraft.io/install/flutter/raspbian
* Install xwindow
  * Its possible you dont need to install it
* Add “video=HDMI-A-1:800x480M@60” to ~/../boot/firmware/cmdline.txt to config the screen
* You can use startx PROGRAM, where PROGRAM is the absolute path to the program you want to display
* Before using the dashboard you must initialize the can line using:
  * sudo /sbin/ip link set can0 up type can bitrate 500000
