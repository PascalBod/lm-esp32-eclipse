### Table of contents

Click on the ![](images/tocIcon.png) icon, on the right-hand side above.

# Overview

This short tutorial describes a way to make a virtual machine (VM) configured for ESP32 software development with Espressif IDE, based on Eclipse. It also explains how to start using it. The virtualization environment is VirtualBox, and the guest machine runs Linux Mint.

Versions are:

* Linux Mint Xfce: 22.1
* Espressif-IDE: 3.2.0
* ESP-IDF: 5.4

# Prerequisites

* Hardware: a 64-bit computer with enough memory so that the VM can be granted 4 GB, with a few tens of GB available on the disk, and one free USB A port
* Hardware (bis): an [Espressif ESP32-C6-DevKitM-1](https://docs.espressif.com/projects/espressif-esp-dev-kits/en/latest/esp32c6/esp32-c6-devkitm-1/index.html) with a USB C cable to connect it to the computer
* Software development competencies: 
  * Basic knowledge of Linux (knowing the most common commands...)
  * Basic knowledge of VirtualBox (knowing how to create a virtual machine...)
  * Good knowledge of one programming language

# Creation of the VM

Check [this guide](https://github.com/PascalBod/lm-vm) to create a Linux Mint Xfce 22.1 VM.

# VM configuration

## Reference documents

* [Espressif-IDE documentation](https://docs.espressif.com/projects/espressif-ide/en/latest/)

## Prerequisites

Start the Software Manager: **Linux Mint Main Menu > Settings > Software Manager**.

Install **Openjdk-21-jdk**.

Install **Python3-venv** and **Python3-pip** packages.

Install **Git** package.

### ESP-IDF prerequisites

```
$ sudo apt-get install git wget flex bison gperf cmake ninja-build ccache libffi-dev libssl-dev dfu-util libusb-1.0-0
```

## Espressif-IDE

[Download the Linux version of the Espressif-IDE](https://docs.espressif.com/projects/espressif-ide/en/latest/downloads.html#downloads).

At the time of writing, the file name is `Espressif-IDE-3.2.0-linux.gtk.x86_64.tar.gz`.

In the file manager, double-click the file and extract the content to the `~/DevTools` directory (to be created).

Add a launcher to the main menu:
* Right click on the main menu icon and select **Edit Applications**
* Select the `Development` directory
* Click the **+** tool and select **Add Launcher**
* For **Command**, select `/home/developer/DevTools/Espressif-IDE/espressif-ide`
* Click the launcher icon and select `/home/developer/DevTools/Espressif-IDE/icon.xpm`
* Click the `New Launcher` string and replace it by `Espressif-IDE`
* Click the `Add comment` string and replace it by `Espressif-IDE`
* Click the **Save Launcher** tool
* Close the window

# Espressif-IDE configuration

Start Espressif-IDE with the launcher you just created.

Modify the proposed workspace path, replacing it with `/home/developer/Dev/workspace`.

Follow the instructions of the [*ESP-IDF and Tools Installation*](https://docs.espressif.com/projects/espressif-ide/en/latest/installation.html).

A few notes about the above procedure:
* Set the ESP-IDF download directory to `/home/developer/DevTools`
* The **Console** view displays the following messages:
```
Copying OpenOCD Rules
Copying File: /home/developer/.espressif/tools/openocd-esp32/v0.12.0-esp32-20241016/openocd-esp32/bin/../share/openocd/contrib/60-openocd.rules to destination: /etc/udev/rules.d/60-openocd.rules
Unable to copy rules for OpenOCD to system directory, try running the eclipse with sudo command
```

In a terminal, run the command as requested:
```shell
$ sudo cp /home/developer/.espressif/tools/openocd-esp32/v0.12.0-esp32-20241016/openocd-esp32/bin/../share/openocd/contrib/60-openocd.rules /etc/udev/rules.d/60-openocd.rules
```

Close the **ESP-IDF Manager** tab.

# ESP32-C6-DevKitM-1 connection

Connect the board to a USB port of the computer. Use the board USB port marked **USB**.

Check that the virtual machine can see it, with **Devices > USB**. A new USB device should be visible: **Espressif USB JTAG/serial debug unit**. Tick the associated checkbox.

You can assign the board to the virtual machine on a permanent basis with **Devices > USB > USB Settings...**.

# Sample application

[Create a new project](https://docs.espressif.com/projects/espressif-ide/en/latest/startproject.html#create-a-new-project), choosing the *hello_world* template.

Build the project, as explained [here](https://docs.espressif.com/projects/espressif-ide/en/latest/buildproject.html#build-the-project).

Flash the project, as explained [here](https://docs.espressif.com/projects/espressif-ide/en/latest/flashdevice.html#flash-onto-the-device). You may be ask to select the serial port to use. Select the port with a name similar to `/dev/ttyACM0`.
