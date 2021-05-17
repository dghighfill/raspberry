# Installing Ansible on the Raspberry Pi
```
$ sudo apt update
$ sudo apt install -y ansible sshpass
```

This will install the base version of Ansible

Edit the following file `sudo nano /etc/apt/sources.list` and follow these [instructions](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-ansible-on-debian) for Debian.

## Running the first playbook
For all the initial configuration the Pi needs, this is already in a series of playbooks.  `run_play.sh` will invoke the needed playbooks to setup the Pi

```
$ ./run_play.sh
```
