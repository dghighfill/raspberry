# raspberry
A GitHub repo to manage my raspberry pi passion

## Initial Setup
Download [NOOBS](https://www.raspberrypi.org/downloads/noobs/) from and you just need
to unzip this file to a newly formatted SD card.  Make sure the space for the SD Card
is fully allocation to a single partition otherwise you may not get the full use of the
card.  NOOBS will allocate the drive upon installation.

When you start the Rasperry PI with NOOBS you will be prompted for which OS that you want
to install.  Select one and this process can take quite a while (e.g. 45 minutes or so) 
depending on the speed of your PI and card.

After the the OS has been loaded the PI will restart and then there is some additional
configuration that is required.

### Default User ID and Passwrod
**Raspian User Id & Password**
* user id = pi
* password = rapsberry 

### Update the PI First thing
Keep PI up to date - Just do this when you setup the PI first time otherwise packages may not intsall
- sudo apt-get update
- sudo apt-get upgrade

### Turn on SSH
```
$ sudo raspi-config
```
* Option 5
* Option P2 to turn on remote command line access to your Pi using SSH.
	
### Setting the IP Address
To determine the IP address use *ifconfig* and either look for *eth0* or the *wlan0* for
the correct ip of the pi.

```
$ ifconfig 
```

#### Static IP
Two options.  Either at the Network level or at the Raspberry Pi level

Network: To setup a static IP address it was easiest to reserve the IP in Google Home.  Just 
go to the Google Home setup find the devices on the network and then find raspberrypi.  
Reserve the IP by clicking on the three dots up in the corner.

Raspberry Pi: To assign a static IP address.  
https://pimylifeup.com/raspberry-pi-static-ip-address/

### Remote Control with xrdp

Install tightvncserver and xrpd so that you can RDP from a Windows machine.  
```
$ sudo apt-get install tightvncserver
$ sudo apt-get remove xrdp
$ sudo apt-get install xrdp
```

Restart pi and enter the following to make sure its running as a service
```
$ systemctl status xrdp
```

### Bash Setup
Add this to your .bash_profile so that all terminal windows behave the same.
```
# Put any customization is the .bashrc file and just source it here if you logon.
if [ -f $HOME/.bashrc ]; then
        source $HOME/.bashrc
fi
```

### Add Scripts to your path
In the .bashrc_local add the following
```
export PATH=~Development/Scripts:$PATH
```

TODO
Document the setting up of aliases. GiT Push/Pull, etc.
How to define a set of scripts for the path
Install FileZilla on the host computer to transfer files.
