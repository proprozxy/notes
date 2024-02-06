## Install Ubuntu 20.04 in a CUDA compatible way

*for Ubuntu 20.04 LTS*

*from USB drive*

**STEP 1: Preparations**

Insert the bootable Ubuntu USB drive

F2 enter UEFI Settings

F7 enter Advanced Mode

​	Security - Secure Boot - Disabled - F10 Save

​	Set SanDisk as Boot Option #1 - F10 Save

F8 enter Boot Menu

​	Select SanDisk

**STEP 2: Install Ubuntu**

Enter GRUD menu

​	Press 'E' to edit

​	Find line 'file=/cdro/preseed/ubuntu.seed maybe-ubiquity quiet splash ---'

​	Delete '---' and add 'nouveau.modeset=0' to disable the default driver 

​	The line will be like 'file=/cdro/preseed/ubuntu.seed maybe-ubiquity quiet splash nouveau.modeset=0'

​	F10 to boot

Install Ubuntu

Remove the installation USB and restart

**STEP 3: Install CUDA**

Install CUDA dependencies

```bash
sudo apt-get update -y
sudo apt upgrade -y
sudo apt-get install build-essential ca-certificates g++ curl -y
sudo apt-get install -y software-properties-common
```

Remove older/other CUDA

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

**The instructions** include base installer and driver installer. e.g.

![image](img/Install%20Ubuntu%2020.04%20in%20a%20CUDA%20compatible%20way/CUDA%20Toolkit.png)

Restart

```bash
sudo reboot
```

Check whether it works properly

```bash
nvidia-smi
```
