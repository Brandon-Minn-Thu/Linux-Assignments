# Assignment 3

For **Assignment 3** we were tasked to create users and use created users to test out file access permissions.

## Step 1: Create the Tupu user using the **adduser** script

In this step, we were tasked to use **adduser** script and add user tupu.

```
brandon@brandon-ubuntu-vm-robotics:~$ cd ..
brandon@brandon-ubuntu-vm-robotics:/home$ sudo adduser tupu
info: Adding user `tupu' ...
info: Selecting UID/GID from range 1000 to 59999 ...
info: Adding new group `tupu' (1002) ...
info: Adding new user `tupu' (1002) with group `tupu (1002)' ...
info: Creating home directory `/home/tupu' ...
info: Copying files from `/etc/skel' ...
New password:
Retype new password:
passwd: password updated successfully
Changing the user information for tupu
Enter the new value, or press ENTER for the default
        Full Name []:
        Room Number []:
        Work Phone []:
        Home Phone []:
        Other []:
Is the information correct? [Y/n] Y
info: Adding new user `tupu' to supplemental / extra groups `users' ...
info: Adding user `tupu' to group `users' ...
brandon@brandon-ubuntu-vm-robotics:/home$
```

## Step 2: Create the Lupu user using the useradd command. Try to create a user profile, home directory, and user group similar to Tupu

In the second step, we were tasked to add **lupu** with _useradd_ command.

```
brandon@brandon-ubuntu-vm-robotics:/home$ sudo groupadd lupu
brandon@brandon-ubuntu-vm-robotics:/home$ sudo useradd -m -d /home/lupu -s/bin/bash -g lupu lupu
brandon@brandon-ubuntu-vm-robotics:/home$ sudo passwd lupu
New password:
Retype new password:
passwd: password updated successfully
brandon@brandon-ubuntu-vm-robotics:/home$ id lupu
uid=1021(lupu) gid=1021(lupu) groups=1021(lupu)
brandon@brandon-ubuntu-vm-robotics:/home$
```

## Step 3: Create the Hupu system user with the login shell set to /bin/false

In this step, we were tasked to create hupu system using "_/bin/false_"

```
brandon@brandon-ubuntu-vm-robotics:/home$ sudo useradd --system --shell /bin/false hupu
brandon@brandon-ubuntu-vm-robotics:/home$ id
uid=1000(brandon) gid=1020(mickey) groups=1020(mickey),4(adm),24(cdrom),27(sudo),30(dip),105(lxd),1000(brandon)
brandon@brandon-ubuntu-vm-robotics:/home$
```

## Step 4: Add the users Tupu and Lupu to the sudo users

In this step, we are given two options to add the users:

First one:
```
sudo visudo
```
After this:
```
Add the following lines:
tupu ALL=(ALL:ALL) ALL
lupu ALL=(ALL:ALL) ALL
```

Second one:
```
sudo usermod -aG sudo tupu
sudo usermod -aG sudo lupu
```

I decided to use the second solution for this step

```
brandon@brandon-ubuntu-vm-robotics:/home$ sudo usermod -aG sudo tupu
brandon@brandon-ubuntu-vm-robotics:/home$ sudo usermod -aG sudo lupu
brandon@brandon-ubuntu-vm-robotics:/home$ groups tupu
tupu : tupu sudo users
brandon@brandon-ubuntu-vm-robotics:/home$ groups lupu
lupu : lupu sudo
brandon@brandon-ubuntu-vm-robotics:/home$
```

## Step 5: Create a directory /opt/projekti and add both users (Tupu and Lupu) as owners. Only Tupu and Lupu should have access to list files in the directory, read, and modify them

Firstly, I created. a group for both Tupu and Lupu.

```
sudo groupadd projekti
```

And added both users to the group:

```
sudo usermod -aG projekti tupu
sudo usermod -aG projekti lupu
```

After this, I created a projekti directory:
```
sudo mkdir /opt/projekti
```

Next, I assigned group ownership:
```
sudo chown root:projekti /opt/projekti
```

After doing this, I set the directory permissions
```
sudo chmod 770 /opt/projekti
```

With this, setgid bit ensures all newly created files and directories inherit the _projekti_ group
```
sudo chmod g+s /opt/projekti
```

```
brandon@brandon-ubuntu-vm-robotics:/home$ sudo groupadd projekti
brandon@brandon-ubuntu-vm-robotics:/home$ sudo usermod -aG projekti tupu
brandon@brandon-ubuntu-vm-robotics:/home$ sudo usermod -aG projekti lupu
brandon@brandon-ubuntu-vm-robotics:/home$ getent group projekti
projekti:x:1022:tupu,lupu
brandon@brandon-ubuntu-vm-robotics:/home$ sudo mkdir /opt/projekti
brandon@brandon-ubuntu-vm-robotics:/home$ sudo chown root:projekti /opt/projekti
brandon@brandon-ubuntu-vm-robotics:/home$ sudo chmod 770 /opt/projekti
brandon@brandon-ubuntu-vm-robotics:/home$ sudo chmod g+s /opt/projekti
brandon@brandon-ubuntu-vm-robotics:/home$ ls -ld /opt/projekti
drwxrws--- 2 root projekti 4096 Feb 16 17:56 /opt/projekti
brandon@brandon-ubuntu-vm-robotics:/home$
```

## Step 6: Permission Testing

I wanted to test if everything works perfectly or not
- Test as _tupu_

```
su - tupu
cd /opt/projekti
touch test_tupu.txt
ls -l
```

```
brandon@brandon-ubuntu-vm-robotics:/home$ su - tupu
Password:
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

tupu@brandon-ubuntu-vm-robotics:~$ cd /opt/projekti
tupu@brandon-ubuntu-vm-robotics:/opt/projekti$ touch test_tupu.txt
tupu@brandon-ubuntu-vm-robotics:/opt/projekti$ ls -l
total 0
-rw-rw-r-- 1 tupu projekti 0 Feb 16 18:00 test_tupu.txt
tupu@brandon-ubuntu-vm-robotics:/opt/projekti$ logout
brandon@brandon-ubuntu-vm-robotics:/home$ cd
brandon@brandon-ubuntu-vm-robotics:~$
```

- Test as _lupu_

```
su - lupu
cd /opt/projekti
echo "hello" >> test_tupu.txt
touch test_lupu.txt
ls -l
```

```
brandon@brandon-ubuntu-vm-robotics:~$ su - lupu
Password:
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

lupu@brandon-ubuntu-vm-robotics:~$ cd /opt/projekti
lupu@brandon-ubuntu-vm-robotics:/opt/projekti$ echo "hello" .. test_tupu.txt
hello .. test_tupu.txt
lupu@brandon-ubuntu-vm-robotics:/opt/projekti$ touch test_lupu.txt
lupu@brandon-ubuntu-vm-robotics:/opt/projekti$ ls -l
total 0
-rw-rw-r-- 1 lupu projekti 0 Feb 16 18:05 test_lupu.txt
-rw-rw-r-- 1 tupu projekti 0 Feb 16 18:00 test_tupu.txt
lupu@brandon-ubuntu-vm-robotics:/opt/projekti$ logout
brandon@brandon-ubuntu-vm-robotics:~$
```

- Test as_hupu_

```
su - hupu
cd /opt/projekti
```

```
brandon@brandon-ubuntu-vm-robotics:~$ su - hupu
Password:


su: Authentication failure
brandon@brandon-ubuntu-vm-robotics:~$
```

_tupu_ and _lupu_ allows access but for _hupu_, it denies, which shows that the assignment works perfectly.

## Conclusion

This task helps us learn how to manage linux users and permission using users, sudo access, groups, and directory permission control