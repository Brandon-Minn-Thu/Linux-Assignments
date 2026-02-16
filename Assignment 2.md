# Assignment No 2

For the second assignment, our instructor has given us an assignment where we need to select 5 different **Level 2** directories and save their contents in one file named _listing.md_.

Below are my lines of codes for the homework:
```
brandon@brandon-ubuntu-vm-robotics:~$ ls /
bin                home               media  run                 sys
bin.usr-is-merged  lib                mnt    sbin                tmp
boot               lib.usr-is-merged  opt    sbin.usr-is-merged  usr
dev                lib64              proc   snap                var
etc                lost+found         root   srv
brandon@brandon-ubuntu-vm-robotics:~$ ls /home
brandon  mickey  pluto
brandon@brandon-ubuntu-vm-robotics:~$ ls /var
backups  crash  local  log   opt  snap   tmp
cache    lib    lock   mail  run  spool
brandon@brandon-ubuntu-vm-robotics:~$ ls /run
1_waagent.pid    lock                  snapd-snap.socket
agetty.reload    log                   snapd.socket
blkid            lvm                   sshd
chrony           lxd-installer.socket  sshd.pid
cloud-init       motd.d                sudo
console-setup    motd.dynamic          systemd
credentials      mount                 tmpfiles.d
crond.pid        multipath             ubuntu-advantage
crond.reboot     multipathd.pid        udev
cryptsetup       needrestart           udisks2
dbus             reboot-required       user
dhcpcd           reboot-required.pkgs  utmp
dmeventd-client  screen                uuidd
dmeventd-server  sendsigs.omit.d       waagent.pid
fsck             setrans
initctl          shm
brandon@brandon-ubuntu-vm-robotics:~$ cd /home/brandon
brandon@brandon-ubuntu-vm-robotics:~$ cd /home/mickey
brandon@brandon-ubuntu-vm-robotics:/home/mickey$ cd /usr/bin
brandon@brandon-ubuntu-vm-robotics:/usr/bin$ cd /usr/games
brandon@brandon-ubuntu-vm-robotics:/usr/games$ cd /var/log
brandon@brandon-ubuntu-vm-robotics:/var/log$ cd ~
brandon@brandon-ubuntu-vm-robotics:~$ mkdir listing.md
brandon@brandon-ubuntu-vm-robotics:~$ rm -rf listing.md
brandon@brandon-ubuntu-vm-robotics:~$ > listing.md
brandon@brandon-ubuntu-vm-robotics:~$ # Start fresh
echo "## /home/brandon" > listing.md
ls -1 /home/brandon >> listing.md
echo "" >> listing.md

echo "## /home/mickey" >> listing.md
sudo ls -1 /home/mickey >> listing.md
echo "" >> listing.md

echo "## /usr/bin" >> listing.md
ls -1 /usr/bin >> listing.md
echo "" >> listing.md

echo "## /usr/games" >> listing.md
ls -1 /usr/games >> listing.md
echo "" >> listing.md

echo "## /var/log" >> listing.md
ls -1 /var/log >> listing.md
brandon@brandon-ubuntu-vm-robotics:~$ ls listing.md
listing.md
brandon@brandon-ubuntu-vm-robotics:~$ less listing.md
brandon@brandon-ubuntu-vm-robotics:~$
```
