## NVIDIA Driver Installation

检查是否安装显卡驱动

```cmd
nvidia-smi
```

从硬件级别检测显卡

```cmd
lspci | grep -i nvidia
```

根据 PCI 号查询对应的显卡型号

[PCI devices (ucw.cz)](https://admin.pci-ids.ucw.cz//mods/PC/10de?action=help?help=pci)

根据显卡型号查询对应驱动版本

[Official Drivers | NVIDIA](https://www.nvidia.com/Download/index.aspx)

可通过图形化界面或命令行安装驱动

图形化界面

命令行

检查可安装的驱动

```cmd
ubuntu-drivers devices
```

```cmd
sudo apt install nvidia-driver-xxx
```

或自动安装系统推荐驱动

```cmd
sudo ubuntu-drivers autoinstall
```



重新启动后运行

```cmd
nvidia-smi
```

可显示结果则安装成功且驱动已运行



如重新启动后黑屏，参考解决方案

如报错

```
NVIDIA-SMI has failed because it couldn't communicate...
```



检查 NVIDIA 内核是否成功加载

```cmd
lsmod | grep nvidia
```

如无输出，尝试手动启动

```cmd
sudo modprobe nvidia
```

报错

```cmd
Operation not permitted
```



大致有 3 种情况



Nouveau 未禁用

Nouveau 是 NVIDIA GPU 的开源驱动程序。如果系统同时安装了 Nouveau 和官方 NVIDIA 驱动，可能会导致冲突。通常，需要将 Nouveau 加入黑名单，禁止它在系统启动时加载。

检查 Nouveau 是否已禁用

```cmd
lsmod | grep nouveau
```

如无输出，则说明已禁用



系统内核版本与驱动版本冲突

NVIDIA 驱动对内核版本有特定的要求。如果内核更新了，而 NVIDIA 驱动没有相应更新，或者驱动不兼容当前内核版本，可能会导致 NVIDIA 驱动无法正确加载。

```cmd
uname -r
```

```cmd
sudo apt install dkms
```

```cmd
dkms status nvidia
```

```cmd
dpkg --get-selections | grep linux-image 
```



SecureBoot 阻止了驱动加载

如果启用了 Secure Boot，系统可能会阻止未签名的驱动加载。NVIDIA 驱动需要在 Secure Boot 禁用或正确配置的环境中加载。

检查 SecureBoot

```cmd
mokutil --sb-state 
```

SecureBoot enabled



解决方案

重新启动时，按住`shift`（部分系统为`esc`）访问 GRUB 菜单，选择`Advanced options for Ubuntu`，进入指定内核的`Recovery Mode`，选择`root`进入命令行，输入以下代码卸载已安装的驱动

```cmd
sudo apt-get --purge remove nvidia*
sudo apt-get --purge remove "*nvidia*"
sudo apt autoremove
```

通过图形化界面下载

设置 SecureBoot 的密码

重新启动

选择 Enroll MOK 输入密码

选择 reboot

