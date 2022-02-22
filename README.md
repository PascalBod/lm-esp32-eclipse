#### Table of contents

* [Overview](#overview)
* [Prerequisites](#prerequisites)
* [Creation of the VM](#creationOfTheVm)
* [VM configuration](#vmConfiguration)
  * [Reference documents](#referenceDocuments)
  * [Prerequisites](#prerequisites)
    * [Python](#python)
    * [Eclipse](#eclipse)
    * [Git](#git)
  * [Eclipse IDF plugin](#eclipseIdfPlugin)
  * [ESP-IDF installation](#espIdfInstallation)
  * [Tools installation](#toolsInstallation)
* [ESP32-DevKitC connection](#esp32devkitcConnection)
* [Sample application](#sampleApplication)
* [Upgrade](#upgrade)

<a name="overview"></a>
# Overview

This short tutorial describes a way to make a virtual machine configured for ESP32 software development with Eclipse, and explains how to start using it. The virtualization environment is VirtualBox, and the guest machine runs Linux Mint.

Versions are:

* Linux Mint: 20.3
* Eclipse for C/C++ Developers: 2021‑09 R
* Eclipse IDF plugin: 2.4.1
* ESP-IDF: 4.4

<a name="prerequisites"></a>
# Prerequisites

* hardware: a 64-bit computer with enough memory so that the VM can be granted 8 GB, with a few tens of GB available on the disk, and one free USB A port
* hardware (bis): an [Espressif ESP32-DevKitC](https://www.espressif.com/en/products/devkits/esp32-devkitc) with an USB A / micro USB B cable - any similar development board can be used
* software development competencies: 
  * basic knowledge of Linux (knowing the most common commands...)
  * basic knowledge of VirtualBox (knowing how to create a virtual machine...)

<a name="creationOfTheVm"></a>
# Creation of the VM

Check [this guide](https://github.com/PascalBod/lm-vm) to create a Linux Mint 20.3 VM.

<a name="vmConfiguration"></a>
# VM configuration

<a name="referenceDocuments"></a>
## Reference documents

* [Espressif documentation](https://github.com/espressif/idf-eclipse-plugin)

<a name="prerequisite"></a>
## Prerequisites

<a name="python"></a>
### Python

Latest Linux Mint versions (20.n) come with python3. Define the **python** command so that it runs python3 by installing the **python-is-python3** package:

```shell
$ sudo apt-get install python-is-python3
```

Additionally, install the **python3-virtualenv** package:

```shell
$ sudo apt-get install python3-virtualenv
```

<a name="eclipse"></a>
### Eclipse

Go to the [Eclipse Installer download page](https://www.eclipse.org/downloads/packages/installer) and click on the [Eclipse 2021-09 (4.21) link](https://www.eclipse.org/downloads/packages/release/2021-09/r). Download the installer (Linux x86_64).

Check the integrity of the downloaded file.

Create the **~/DevTools** directory, and extract the contents of the downloaded file into it.

Run `~/DevTools/eclipse-installer/eclipse-inst`.

Choose **Eclipse IDE for C/C++ Developers**. Keep the default path values.

Click on the **Install** button, accept the license.

At the end of the installation, you can choose to launch Eclipse, and keep it open for next steps.

<a name="git"></a>
### Git

Install git:

```shell
$ sudo apt-get install git
```

<a name="eclipseIdfPlugin"></a>
## Eclipse IDF plugin

Start Eclipse, if not yet done from the installer. Keep the proposed workspace. Close the **Welcome** tab and then the **Donate** tab.

[Install the IDF plugin](https://github.com/espressif/idf-eclipse-plugin#installing-idf-plugin-using-update-site-url) (stable release). At time of writing, this is version 2.4.1.

Restart Eclipse.

<a name="espIdfInstallation"></a>
## ESP-IDF installation

[Install ESP-IDF from Eclipse](https://github.com/espressif/idf-eclipse-plugin#installing-esp-idf). Choose `v4.4` for the version, and select the `DevTools` directory as download directory.

<a name="toolsInstallation"></a>
## Tools installation

A message box offers to download the tools. Click on the **Yes** button. In the **Install Tools** dialog box that appears, click on **Install Tools** button.

<a name="esp32devkitcConnection"></a>
# ESP32-DevKitC connection

Connect the DevKitC board to a USB port of the computer. Check that the virtual machine can see it, with **Devices > USB**. A new USB device should be visible: *Silicon Labs CP2102N USB to UART Bridge Controller*. Tick the associated checkbox.

You can assign the board to the virtual machine on a permanent basis with **Devices > USB > USB Settings...**.

<a name="sampleApplication"></a>
# Sample application

[Create a new project](https://github.com/espressif/idf-eclipse-plugin#create-a-new-project-using-esp-idf-templates), choosing the *hello_world* template.

[Configure a launch target](https://github.com/espressif/idf-eclipse-plugin#configuring-launch-target) for the board. Build the project, as explained [here](https://github.com/espressif/idf-eclipse-plugin#compiling-the-project).

Flash the project, as explained [here](https://github.com/espressif/idf-eclipse-plugin#flashing-the-project). If the console shows that the flashing operation does not start right after having requested it, i.e. the console waits on `Connecting........_____...`, hold down the board BOOT button until the flashing operation starts (a little bit more than 1 s). 

To display trace messages printed by the application, [start a terminal](https://github.com/espressif/idf-eclipse-plugin#viewing-serial-output).

<a name="upgrade"></a>
# Upgrade

To upgrade ESP-IDF, select **Espressif > Download and Configure ESP-IDF** and select the ESP-IDF version to download. Once downloaded, the ESP-IDF plugin might ask you to install a new set of tools. Accept, and install the tools. 

To upgrade the Eclipse IDF plugin, check [this section](https://github.com/espressif/idf-eclipse-plugin#how-do-i-upgrade-my-existing-idf-eclipse-plugin).
