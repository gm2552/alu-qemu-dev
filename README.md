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
wget https://github.com/gm2552/alu-qemu-dev/raw/master/flash1.img.zip
unzip flash0.img.zip
unzip flash1.img.zip
```

### Download Ubuntu Cloud Image File
You can use pretty much any Ubuntu cloud image, but 16.04 is the recommended image.  Download the Ubuntu Cloud image using the following command.

```
cd ~/alu-emu
wget https://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-arm64-uefi1.img
```

### Launch The Emulator

You are now ready to launch the emulator.  Qemu has several switching that you can lookup to tweak how you want your emulator to run.  The following is a default configuration that runs 4 virtual processes using 2GB of memory.  You will not be able to ssh or sftp into this emulator.  Instead it will run like you were at an actual terminal.  However, you CAN access the network from inside the emulator assuming that your Ubuntu host has network capabilities.

```
qemu-system-aarch64 -m 2048 -smp 4 -cpu cortex-a57 -M virt -nographic   -pflash flash0.img   -pflash flash1.img   -drive if=none,file=ubuntu-16.04-server-cloudimg-arm64-uefi1.img,id=hd0   -device virtio-blk-device,drive=hd0   -drive if=none,id=cloud,file=cloud.img   -device virtio-blk-device,drive=cloud   -netdev user,id=user0 -device virtio-net-device,netdev=user0
```

During the bootup sequence, you may see message error message like no video found or press any key.  You can ignore these and the system will continue to load.  It may take 3-5 minutes for the system to load.  You will NOT be able to login for the first time until you see a log message that says "END SSH HOST KEY KEYS."  The system needs to apply the default user configuration and passwork from the cloud.img file which can take a little longer the first time the system boots.

After the system completes booting, you can use the following credentials to log in.  NOTE: You may need to hit the return key a couple of times to bring up the login prompt.

```
user: ubuntu
password: asdfqwer
```
