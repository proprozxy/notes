## Install Ubuntu 20.04 in a CUDA compatible way

*for ubuntu 20.04 lts*

*from USB drive*

**STEP 1: Preparations**

Insert the bootable Ubuntu USB drive

F2 enter UEFI Settings

F7 enter Advanced Mode

​	Security - Secure Boot - Disabled - F10 Save

​	Set SanDisk at Boot Option #1 - F10 Save

F8 enter Boot Menu

​	Select SanDisk

**STEP 2: Install Ubuntu**

Goes to GRUD menu

​	Press 'E' to edit

​	Find line 'file=/cdro/preseed/ubuntu.seed maybe-ubiquity quiet splash ---'

​	Delete '---' and add 'nouveau.modeset=0' to disable the default driver 

​	The line will be like 'file=/cdro/preseed/ubuntu.seed maybe-ubiquity quiet splash nouveau.modeset=0'

​	F10 to boot

Install ubuntu

Remove the installation USB and restart

**STEP 3: Install Cuda**

Install cuda dependencies

```bash
sudo apt-get update -y
sudo apt upgrade -y
sudo apt-get install build-essential ca-certificates g++ curl -y
sudo apt-get install -y software-properties-common
```

Remove older/other cuda

```bash
sudo apt-get purge nvidia*
sudo apt-get autoremove
sudo apt-get autoclean
sudo rm -rf /usr/local/cuda*
sudo apt-get --purge remove "*cublas*" "*cufft*" "*curand*" "*cusolver*" "*cusparse*" "*npp*" "*nvjpeg*" "cuda*" "nsight*"
sudo apt-get --purge remove "*nvidia*"
sudo apt-get autoremove 
```

Go [CUDA Toolkit Downloads | NVIDIA Developer](https://developer.nvidia.com/cuda-downloads) to choose version then follow **the instructions** to install

**The instructions** include 2 parts: base installer and driver installer. e.g.

![cuda toolkit](.\img\Install Ubuntu 20.04 in a CUDA compatible way on RTX 30 series laptops\cuda toolkit.png)

Restart

```bash
sudo reboot
```

Check whether it works properly

```bash
nvidia-smi
```
