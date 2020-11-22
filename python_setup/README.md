# Python for the Raspberry Pi
Enther python from a terminal window to determine what version you are on.

If you're on Python 2 and want Python 3 to be the default.

1. Enter directory /usr/bin
`cd /usr/bin`

Check to see what the symlink points to.  The l if the `lrwxrwxrwx` means its a link.
```
pi@raspberrypi:/usr/bin $ ls -la python
lrwxrwxrwx 1 root root 7 Jul  5 13:38 python -> python2
```

NOTE: Ansible doesn't seem to run on Python3 so this might cause you some issues.

2. Delete the old python link
`sudo rm python`

3. Create new python symbolic link to python3.
`sudo ln s python3 python`

Now run the command again.
```
pi@raspberrypi:/usr/bin $ ls -la python
lrwxrwxrwx 1 root root 7 Jul  5 13:38 python -> python3
```

4. Execute python to check whether the link succeeds.
python



