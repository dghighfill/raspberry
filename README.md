# Raspbery Pi Setup
This is a GitHub repo to manage my raspberry pi passion. About every six months I
pick up my Raspberry Pi, want to rebuild it from scratch and messaround with it. 
This repo is dedicated to expediting that setup.  There are set of things that
I have learned over the years to increas my productivity so I try to bake this into the setup
so that I can be up and running as soon as possible.

## Initial Setup
Download [NOOBS](https://www.raspberrypi.org/downloads/noobs/) and you just need
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
It's probably best to keep the .bashrc in its original form and just source another
file.  This helps with future upgrades and then you have all your customizations 
in one spot.

If you don't have a `~/.bash_profile`, then create one.

Add this to your .bash_profile so that all terminal windows behave the same.
```
# Load the .bashrc file if you logon remotly from SSH.
if [ -f $HOME/.bashrc ]; then
        source $HOME/.bashrc
fi
```

At the bottom of the `.bashrc` add the following line and this will enable us to keep 
all our custom bash behavior in one file.

```
source .bashrc_local
```

### .bashrc_local
This file is full of the customization that we want to add to bash.  Here are some examples
```
# Put any Scripts that we want to run in our system path.
export PATH=~/Development/Scripts:$PATH

# Add the Git Branch to the Prompt
# Show current git branch in command line
# https://unix.stackexchange.com/questions/124407/what-color-codes-can-i-use-in-my-ps1-prompt
parse_git_branch() {
     git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}
export PS1="\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\[\033[33m\]\$(parse_git_branch)\[\033[00m\] $ "

# All my really cool aliases
alias gs='echo "git status" && git status'
alias gpl='echo "git pull" && git pull'
alias gps='echo "git push" && git push origin'
alias gc='echo "git commit w/message" && git commit -m $1'
alias gr='echo "git revert" && git reset --soft HEAD~1'

alias sa='ssh-add ~/.ssh/id_rsa'
```

### File Transfer
Install FileZilla on the host computer to transfer files to the Raspberry Pi.
