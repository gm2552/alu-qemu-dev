# alu-qemu-dev
Configuration and required files for creating an A53 dev system with qemu.

## Synopsis
This instructions outline how to install and configure the qemu emulator for an A53 process to build cores and potentially other applications for the AtGames legends ultimate console.  It it mearly used as a build system as testing capabilities are limited with the emulator.

## Needed Resources

### Emulator
You will need a system capabile of running the qemu emulator.  Although not required, these instructions are focused on loading the emulator utilizing Ubuntu.  

### CPU
Emulators are notoriously slow compared to their real hardware counterparts, so a decent and modern CPU with multiple cores (at least 4) is recomended, but not required

### Free Disk space
The default emulator image is relatively small in terms disk space, so you are going to want to increase its size after you get it loaded up for the first time.  

### Memory
Having at least 2 GB of free memory is recomended to build large cores.  

### Unzip and wget programs
Make sure you have an unzip program installed on your machine (or virtual machine) that will running the emulator.  On Ubuntu, this can be done by running the following command:

```
sudo apt-get install -y unzip wget
```

## Installation

Again, these instructions assume you are using Ubuntu, but it is possible to do this on other operating system.  Installing and getting Ubuntu up and running is assumed and beyond the scope of these instructions.

### Install Qemu

Install qemu using the following command:

```
sudo apt-get install -y qemu-system-aarch64
```

### Download Flash and Cloud Image files

For your emulator image files, you will probably want to create a directory to organize your files.  You can use whatever you want, but for these instructions, I will use a directory called alu-emu.  Create this directory with the following command

```
mkdir ~/alu-emu
```

Now download and unzip the image files with the following commands:

```
cd ~/alu-emu
wget https://github.com/gm2552/alu-qemu-dev/raw/master/cloud.img
wget https://github.com/gm2552/alu-qemu-dev/raw/master/flash0.img.zip
wget https://github.com/gm2552/alu-qemu-dev/blob/master/flash1.img.zip
unzip flash0.img.zip
unzip flash1.img.zip
```
