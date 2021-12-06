[![Linux](https://svgshare.com/i/Zhy.svg)](https://svgshare.com/i/Zhy.svg) [![Maintenance](https://img.shields.io/badge/Maintained%3F-yes-green.svg)](https://GitHub.com/Naereen/StrapDown.js/graphs/commit-activity)

# HomeSeer Linux Installer Package/Scripts

(Developed with ♥ by SavageSoftware, LLC.)

> :bomb:  This repository and scripts are considered `EXPERIMENTAL` at this time.  We are not responsible for any data lost or systems corrupted!

---

## TL;DR

Install Homeseer on your (Debian-based) Linux system:
```
curl -sSL https://homeseer.sh/install | sudo bash
```

---

## Contents

 - [Overview](#overview)
   - [Resource Links](#resource-links)
 - [Prerequsites](#prerequsites)
   - [OS/Distribution](#operating-system--distribution)
   - [Update OS](#update-os)
   - [Curl](#curl)
 - [Installation](#automated-installation)
   - [Automated Installation](#automated-installation)
   - [Manual Installation](#manual-installation)
 - [Uninstall](#uninstall)
   - [Uninstallation](#uninstall)
   - [Complete Uninstallation/Removal](#complete-automated-removal--complete-uninstall)
 - [Advanced](#install-explict-versions)
   - [Install Explicit Versions](#install-explict-versions)
   - [Enable Beta/Release Candidate Versions](#enable-betarelease-candidate-versions)
 - [Installation Notes/Details](#installation-notes--details)
   - [Location/Path](#location--path)
   - [Service/Daemon](#service--daemon)
   - [User Account](#user-account)
 - [Service Control](#service-control)
   - [Start](#start-service)
   - [Stop](#stop-service)
   - [Restart](#restart-service)
   - [Status](#service-status)
- [Debian 11 Installation Notes](#debian-11-installation-notes)

---

## Overview

  The purpose of this repository is to host automated installation scripts and APT/PPA repository packages for installing HomeSeer on Debian-based Linux systems.
  The latest official release packages and release notes for HomeSeer can be found at: [https://docs.homeseer.com/display/HSPI/HS4+Release+Notes](https://docs.homeseer.com/display/HSPI/HS4+Release+Notes)
  
  This repository is not supported, sponsored or directly affiliated with Homeseer ([https://homeseer.com/](https://homeseer.com/)).
  
  ### Resource Links
  - WebPage: [https://homeseer.sh](https://homeseer.sh)
  - GitHub Repository: [https://github.com/HomeSeerLinux/homeseerlinux.github.io](https://github.com/HomeSeerLinux/homeseerlinux.github.io)
  - APT/PPA Package Repository: [https://github.com/HomeSeerLinux/download](https://github.com/HomeSeerLinux/download)

---

## Prerequsites

  ### Operating System / Distribution
  
  A Debian-based distribution of Linux is required to use this installation script and APT/PPA repository.
  The following distributions have been tested:
  
  - Ubuntu 20.04
  - Linux Mint 20.2
  - PopOS 21.04
  - Debian 11.1.0 (*The \*.deb package fails to install in Debian GNU 11. [See this section for details on installing on Debian 11](#debian-11-installation-notes)*)

  ### Update OS

  An `sudo apt update && apt upgrade` was performed on each distribution prior to installation.

  ### Curl
  
  Curl must be installed to download and execute the automated installation script.

<br/>

---

## Automated Installation
The following command will use our pre-built installation scripts to install the latest release of Homeseer on your (Debian-based) Linux system:

```bash
curl -sSL https://homeseer.sh/install | sudo bash
```

> :pushpin:  Before running this script blindly with `sudo` privileges on your system, you should inspect the [script contents](https://raw.githubusercontent.com/HomeSeerLinux/homeseerlinux.github.io/main/install) to ensure there are no nefarious or malicious actions taking place.  You can also view the file contents using this command: `curl https://homeseer.sh/install`.


## Manual Installation
If you prefer not to use the simple script above due the the security nature of blindly allowing a script to run with `sudo` privileges, you can also use these commands to setup the appropriate Homeseer.sh APT/PPA repository on your local system:

```bash
wget -qO- https://homeseer.sh/homeseer.gpg | sudo apt-key add -
echo 'deb [arch=all] https://homeseer.sh/download v4 stable' | sudo tee /etc/apt/sources.list.d/homeseer.list
sudo apt update
sudo apt install homeseer
```

<br/>

---

## Uninstall 
The following command will remove the Homeseer application files from your (Debian-based) Linux system:

```bash
sudo apt remove homeseer
```
This method will leave any configurtation files, data files, log files and installed plugin files on the system in the `/opt/HomeSeer` directory.  This method will also leave the Homeseer.sh APT/PPA repository configured in case you wish to re-install HomeSeer later.


## Complete Automated Removal / Complete Uninstall
The following command will use our pre-built uninstallation scripts to remove the HomeSeer application file and Homeseer.sh APT/PPA repository configuration files from your (Debian-based) Linux system:

```bash
curl -sSL https://homeseer.sh/uninstall | sudo bash
```

> :pushpin:  Before running this script blindly with `sudo` privileges on your system, you should inspect the [script contents](https://raw.githubusercontent.com/HomeSeerLinux/homeseerlinux.github.io/main/uninstall) to ensure there are no nefarious or malicious actions taking place.  You can also view the file contents using this command: `curl https://homeseer.sh/uninstall`.


The following command will completely remove/wipe all Homeseer data, log and configutation files from your (Debian-based) Linux system:

```bash
sudo rm -R /opt/HomeSeer
```

The following command will remove/wipe the `homeseer` user account (used by the `homeseer.service` daemon) from your (Debian-based) Linux system:

```bash
sudo deluser homeseer
```

> :warning:  This uninstall script and commands will remove **all** Homeseer application files, data files and configuration files from your local system.  Please backup your Homeseer configuation data before uninstalling using this script/commands.  

<br/>

---

## Install Explict Versions

Once your system has been configured with the Homeseer APT/PPA repository you can use the `apt install` command to install explict versions of Homeseer uisng the `={VERSION}` syntax as shown in the example below.


```bash
sudo apt install homeseer=4.2.0.0
```

<br/>

---

## Enable Beta/Release Candidate Versions

Once your system has been configured with the Homeseer APT/PPA repository you can modify the `/etc/apt/sources.list.d/homeseer.list` file if you would like to enable installing BETA and RELEASE CANDIDATE versions.

1.) Edit the `/etc/apt/sources.list.d/homeseer.list` file using your favorite text editor:
```bash
sudo nano /etc/apt/sources.list.d/homeseer.list
```

2.) Edit the line with the `https://homeseer.sh/download` URI and include the `testing` label/tag at the end of the line as shown below.

```bash
deb [arch=all] https://homeseer.sh/download v4 stable testing
```

3.) Save the updated file and exit the text editor.

4.) Perform an `apt update` to load/refresh the lastest available packages.
```bash
sudo apt update
```

5.) Finally you can install the lastest version using the following command.  
```bash
sudo apt install homeseer
```
  > :pushpin:  _The latest version is determined by the semantic version number.  If an avaialble BETA or RELEASE CANDIDATE version is higher than the lasted release, then that BETA or RC version will be installed._

  Alternatively you can install the explict version using the `={VERSION}` syntax as shown in the example below.

```bash
sudo apt install homeseer=4.2.7.0
```

<br/>

---

## Installation Notes / Details

### Location / Path

The Homeseer Debian installed package will install Homeseer to the following location:

```
/opt/HomeSeer
```

### Service / Daemon

The Homeseer Debian installed package will install a `homeseer.service` (systemd) to run Homeseer automatically on startup and in the background.  The `homeseer.service` (systemd) configuration is stored in the following location:

```bash
/etc/systemd/system/homeseer.service
```

> :mag_right: [View the contents of the `homeseer.service` file here](https://github.com/HomeSeerLinux/download/blob/main/.build/etc/systemd/system/homeseer.service)

On completion of the installation, the Homeseer service should be started automatically. 


### User Account

The Homeseer Debian installed package will create a `homeseer` system user account for use with the `homeseer.service` service/daemon.

<br/>

---

## Service Control

The following commands can be used to `start`, `stop`, `restart` and check the `status` of the Homeseer service/daemon.

### Start Service

You can `start` the Homeseer service using the following command:

```bash
sudo service homeseer start
```

### Stop Service

You can `stop` the Homeseer service using the following command:

```bash
sudo service homeseer stop
```

### Restart Service

<a id="service-restart"/>

You can `restart` the Homeseer service using the following command:

```bash
sudo service homeseer restart
```

### Service Status

You can check the `status` of the Homeseer service using the following command:

```bash
sudo service homeseer status
```

<br/>

---

## Debian 11 Installation Notes

This installation script and \*.deb installer package fails to install on Debian (v11) due to unmet dependencies in the \*.deb installer package.  These dependencies can be install in Debian manually using the following commands:    

1.) Install the Mono framework:   
  ```
  sudo apt update && sudo apt upgrade
  sudo apt install dirmngr gnupg apt-transport-https ca-certificates -y
  sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
  sudo sh -c 'echo "deb https://download.mono-project.com/repo/debian stable-buster main" > /etc/apt/sources.list.d/mono-official-stable.list'
  sudo apt update
  sudo apt install mono-complete -y
  sudo apt install mono-devel -y
  sudo apt install mono-vbnc -y
  ```
  
2.) Install other dependencies:
  ```  
  sudo apt install chromium -y
  sudo apt install alsamixergui -y
  sudo apt install flite -y
  sudo apt install aha -y
  sudo apt install ffmpeg -y
  sudo apt remove britty -y    
  ```

3.) Download the homeseer (\*.deb) debian installation package from the APT/PPA repository:
  ```
  sudo apt download homeseer
  ```
4.) Install the downloaded homeseer (\*.deb) debian installation package with spcial flags to ignore mismatched named dependencies: 
  ```
  sudo dpkg -i --ignore-depends=chromium-browser,alsa-base homeseer_4.2.6.0_all.deb
  ```

---

