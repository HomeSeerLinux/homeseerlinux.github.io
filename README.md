# HomeSeer Linux Installer Package/Scripts

(Developed with ♥ by SavageSoftware, LLC.)

> :bomb:  This repository and scripts are considered `EXPERIMENTAL` at this time.  We are not responsible for any data lost or systems corrupted!

---

## Contents

 - [Overview](#overview)
   - [Resource Links](#resource-links)
 - [Installation](#automated-installation)
   - [Automated Installation](#automated-installation)
   - [Manual Installation](#manual-installation)
 - [Uninstall](#uninstall)
   - [Uninstallation](#uninstall)
   - [Complete Uninstallation/Removal](#complete-automated-removal--complete-uninstall)
 - [Advanced](#install-explict-versions)
   - [Install Explicit Versions](#install-explict-versions)
   - [Enable Beta/Release Candidate Versions](#beta)
 - [Installation Notes/Details](#install-notes)
   - [Location/Path](#install-path)
   - [Service/Daemon](#install-service)
   - [User Account](#install-user)
 - [Service Control](#service)
   - [Start](#service-start)
   - [Stop](#service-stop)
   - [Restart](#service-restart)
   - [Status](#service-status)

---

## Overview

  The purpose of this repository is to host automated installation scripts and APT/PPA repository packages for installing HomeSeer on Debian-based Linux systems.
  The latest official release packages and release notes for HomeSeer can be found at: [https://docs.homeseer.com/display/HSPI/HS4+Release+Notes](https://docs.homeseer.com/display/HSPI/HS4+Release+Notes)
  
  This repository is not supported, sponsored or directly affiliated with Homeseer ([https://homeseer.com/](https://homeseer.com/)).
  
  #### Resource Links
  - WebPage: [https://homeseer.sh](https://homeseer.sh)
  - GitHub Repository: [https://github.com/HomeSeerLinux/homeseerlinux.github.io](https://github.com/HomeSeerLinux/homeseerlinux.github.io)
  - APT/PPA Package Repository: [https://github.com/HomeSeerLinux/download](https://github.com/HomeSeerLinux/download)
   
---

## Automated Installation
The following command will use our pre-built installation scripts to install the latest release of Homeseer on your (Debian-based) Linux system:

```bash
curl -sSL https://homeseer.sh/install | sudo bash
```

> :pushpin:  Before running this script blindly with `sudo` privileges on your system, you should inspect the [script contents](https://raw.githubusercontent.com/HomeSeerLinux/homeseerlinux.github.io/main/install) to ensure there are no nefarious or malicious actions taking place.


## Manual Installation
If you prefer not to use the simple script above due the the security nature of blindly allowing a script to run with `sudo` privileges, you can also use these commands to setup the appropriate Homeseer.sh APT/PPA repository on your local system:

```bash
wget -qO- https://homeseer.sh/homeseer.gpg | sudo apt-key add -
echo 'deb [arch=all] https://homeseer.sh/download v4 stable' | sudo tee /etc/apt/sources.list.d/homeseer.list
sudo apt update
sudo apt install homeseer
```

---

## Uninstall 
The following command will remove the Homeseer application files from your (Debian-based) Linux system:

```bash
sudo apt remove homeseer
```
This method will leave any configurtation files, data files, log files and installed plugin files on the system in the `/opt/HomeSeer` directory.  This method will also leave the Homeseer.sh APT/PPA repository configured in case you wish to re-install HomeSeer later.


## Complete Automated Removal / Complete Uninstall
The following command will use our pre-built uninstallation scripts to completely remove/wipe all Homeseer files (_including configuration and log files_) from your (Debian-based) Linux system:

```bash
curl -sSL https://homeseer.sh/uninstall | sudo bash
```

> :pushpin:  Before running this script blindly with `sudo` privileges on your system, you should inspect the [script contents](https://raw.githubusercontent.com/HomeSeerLinux/homeseerlinux.github.io/main/uninstall) to ensure there are no nefarious or malicious actions taking place.


> :warning:  This uninstall script will remove **all** Homeseer application files, data files and configuration files from your local system.  Please backup your Homeseer configuation data before uninstalling using this script.  This script will also remove the Homeseer.sh APT/PPA repository configuration from your system. 

---

## Install Explict Versions

Once your system has been configured with the Homeseer APT/PPA repository you can use the `apt install` command to install explict versions of Homeseer uisng the `={VERSION}` syntax as shown in the example below.


```bash
sudo apt install homeseer=4.2.0.0
```

---
<a id="beta"/>

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

---
<a id="install-notes"/>

## Installation Notes / Details

<a id="install-path"/>

### Location/Path

The Homeseer Debian installed package will install Homeseer to the following location:

```
/opt/HomeSeer
```

<a id="install-service"/>

### Service / Daemon

The Homeseer Debian installed package will install a `homeseer.service` (systemd) to run Homeseer automatically on startup and in the background.  The `homeseer.service` (systemd) configuration is stored in the following location:

```bash
/etc/systemd/system/homeseer.service
```

> :mag_right: [View the contents of the `homeseer.service` file here](https://github.com/HomeSeerLinux/download/blob/main/.build/etc/systemd/system/homeseer.service)

On completion of the installation, the Homeseer service should be started automatically. 

<a id="install-user"/>

### User Account

The Homeseer Debian installed package will create a `homeseer` system user account for use with the `homeseer.service` service/daemon.

---
<a id="service"/>

## Service Control

The following commands can be used to `start`, `stop`, `restart` and check the `status` of the Homeseer service/daemon.

<a id="service-start"/>

You can `start` the Homeseer service using the following command:

```bash
sudo service homeseer start
```

<a id="service-stop"/>

You can `stop` the Homeseer service using the following command:

```bash
sudo service homeseer stop
```

<a id="service-restart"/>

You can `restart` the Homeseer service using the following command:

```bash
sudo service homeseer restart
```

<a id="service-status"/>

You can chech the `status` of the Homeseer service using the following command:

```bash
sudo service homeseer status
```

---
