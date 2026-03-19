# Assignment 6: APT (Advanced Package Tool)

## Objectives
- Learn to install, update, remove, and search for software using APT  
- Understand repository management and package dependencies  
- Gain hands-on experience troubleshooting package installation issues  

---

# Part 1: Understanding APT & System Updates

## 1. Check APT Version
```bash
apt --version
```


**Image:**
![alt text](<Screenshot 2026-03-19 at 2.29.38 PM.png>)

## Explanation:
This command displays the installed version of **APT** (Advanced Package Tool).
APT is the package manager used in Ubuntu-based systems.


``2. Update Package List``
```bash
sudo apt update
```
Purpose:

- Downloads the latest package lists from repositories

- Refreshes system metadata

- Does NOT install or upgrade any software

``3. Upgrade Installed Packages``
```bash
sudo apt upgrade -y
```
#### Difference between ```update``` and ```upgrade```
| Command       | What It Does               |
| ------------- | -------------------------- |
| `apt update`  | Refreshes package list     |
| `apt upgrade` | Installs available updates |


Simple: 
- ```update``` = check
- ```upgrade```= install

Simple Explanation:

update = check

upgrade = install

```4. View Pending Updates```
```bash
apt list --upgradable
```
Explanation:
Displays all installed packages that have newer versions available.

**Image:**
![alt text](<Screenshot 2026-03-19 at 2.36.29 PM.png>)

## Part 2: Installing & Managing Packages
``1. Search for an Image Editor``
```bash
apt search image editor
```
**Selected Package:**
``gimp``

``2. View Package Details``
```bash
apt show gimp
```
**Key Dependencies:**

- libgimp2.0t64

- gimp-data

- libc6

- libgtk2.0-0t64

- libpng16-16t64

- libjpeg8

- libtiff6

- libwebp7

- zlib1g

- graphviz

- xdg-utils

Explanation:
These dependencies are required for:

Graphical rendering

Image processing

File format support

System integration

```3. Install the Package```
```bash
sudo apt install gimp -y
```
Verify Installation:

gimp --version

Output Example:

GNU Image Manipulation Program version 2.10.36
``4. Check Installed Package Version``
```bash
apt list --installed | grep gimp
```
```Output Example:```
```bash
gimp/noble-updates,now 2.10.36-3ubuntu0.24.04.1 amd64 [installed]
```
``Additional Installed Packages:``

- gimp-data

- libgimp2.0t64

These were installed automatically as dependencies.

## Part 3: Removing & Cleaning Packages
``1. Remove a Package``
```bash
sudo apt remove gimp -y
```
- Removes the program but keeps configuration files

``2. Purge Configuration Files``
```bash
sudo apt purge gimp -y
```

Difference Between remove and purge
Command	Removes
remove	Program files only
purge	Program + configuration files

``3. Remove Unused Dependencies``
```bash
sudo apt autoremove -y
```
- Why this is important:

Dependencies remain after uninstalling a package

autoremove cleans unnecessary packages

Helps keep the system clean

``4. Clean Cached Files``
```bash
sudo apt clean
```
Explanation:

Deletes downloaded package cache files

Frees disk space

Keeps the system tidy

## Part 4: Managing Repositories & Troubleshooting
``1. List APT Repositories``
```bash
cat /etc/apt/sources.list
```
Note:
In Ubuntu 24.04 (Noble), repositories are managed using the newer deb822 format.
They are stored in:
```bash
/etc/apt/sources.list.d/
```

This replaces the traditional flat sources.list file.

``2. Add Universe Repository``
```
sudo add-apt-repository universe
```
Explanation:
The Universe repository provides:

Community-maintained open-source software

Additional applications and libraries

Packages not officially supported by Canonical

``3. Simulate Installation Failure``
```bash
sudo apt install fakepackage
```
**Error Example:**

E: Unable to locate package fakepackage

**Image:**
![alt text](<Screenshot 2026-03-19 at 2.51.57 PM.png>)

``Troubleshooting Steps``

- Check spelling:
```bash
apt search fakepackage
```
- Update package list:
```bash
sudo apt update
```
- Verify repositories:
```bash
cat /etc/apt/sources.list
```
- Check internet connection

# Bonus: Holding a Package
- Hold a Package
```bash
sudo apt-mark hold gimp
```

Result:

gimp set on hold
- Unhold a Package
```
sudo apt-mark unhold gimp
```
**Why Hold a Package?**

- New version may break compatibility

- Software may contain bugs

- Need a specific stable version

- Important for production system stability