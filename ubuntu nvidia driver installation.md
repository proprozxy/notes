## NVIDIA Driver Installation

ubuntu 20.04 lts

#### 准备工作

检查是否安装显卡驱动

```bash
nvidia-smi
```

![Screenshot from 2024-02-05 00-47-19](.\img\ubuntu nvidia driver installation\Screenshot from 2024-02-05 00-47-19.png)

从硬件级别检测显卡

```bash
lspci | grep -i nvidia
```

![Screenshot from 2024-02-05 00-50-00](.\img\ubuntu nvidia driver installation\Screenshot from 2024-02-05 00-50-00.png)

根据 PCI 号查询对应的显卡型号

[PCI devices (ucw.cz)](https://admin.pci-ids.ucw.cz//mods/PC/10de?action=help?help=pci)

根据显卡型号查询对应驱动版本

[Official Drivers | NVIDIA](https://www.nvidia.com/Download/index.aspx)

#### 安装

可通过图形化界面或命令行安装驱动

##### 图形化界面

![Screenshot from 2024-02-05 00-50-58](.\img\ubuntu nvidia driver installation\Screenshot from 2024-02-05 00-50-58.png)

![Screenshot from 2024-02-05 00-53-09](D:\github\notes\img\ubuntu nvidia driver installation\Screenshot from 2024-02-05 00-53-09.png)

##### 命令行

检查可安装的驱动

```bash
ubuntu-drivers devices
```

![Screenshot from 2024-02-05 00-50-37](.\img\ubuntu nvidia driver installation\Screenshot from 2024-02-05 00-50-37.png)

```bash
sudo apt install nvidia-driver-535
```

或自动安装默认推荐驱动

```bash
sudo ubuntu-drivers autoinstall
```

重启后运行

```bash
nvidia-smi
```

可显示结果则安装成功且驱动已运行



#### 问题与解决方案

报错

```
NVIDIA-SMI has failed because it couldn't communicate...
```

![Screenshot from 2024-02-05 01-47-51](.\img\ubuntu nvidia driver installation\Screenshot from 2024-02-05 01-47-51.png)

检查 NVIDIA 内核是否成功加载

```bash
lsmod | grep nvidia
```

如无输出，说明驱动未启动，尝试手动启动

```bash
sudo modprobe nvidia
```

报错

```
...Operation not permitted
```



包括重启后黑屏，大致有 3 种可能性



##### Nouveau 未禁用

Nouveau 是 NVIDIA GPU 的开源驱动程序。如果系统同时安装了 Nouveau 和官方 NVIDIA 驱动，可能会导致冲突。通常，需要将 Nouveau 加入黑名单，禁止它在系统启动时加载。

检查 Nouveau 是否已禁用

```bash
lsmod | grep nouveau
```

![Screenshot from 2024-02-05 01-23-21](.\img\ubuntu nvidia driver installation\Screenshot from 2024-02-05 01-23-21.png)

在终端打开

```bash
sudo gedit /etc/modprobe.d/blacklist.conf
```

在末尾添加

```bash
blacklist nouveau
options nouveau modeset=0
```

返回终端执行命令应用更改

```bash
sudo update-initramfs -u
```

重启后再次验证，如无输出，则说明已禁用



##### 系统内核版本与驱动版本冲突

NVIDIA 驱动对内核版本有特定的要求。如果内核更新后，NVIDIA 驱动没有相应更新，或者驱动不兼容当前内核版本，可能会导致 NVIDIA 驱动无法正确加载。

显示当前正在运行的内核版本号

```bash
uname -r
```

显示与 NVIDIA 显卡驱动相关的 DKMS 模块的当前状态

```bash
dkms status nvidia
```

列出所有已安装的系统内核

```bash
dpkg --get-selections | grep linux-image 
```

![Screenshot from 2024-02-05 01-53-41](.\img\ubuntu nvidia driver installation\Screenshot from 2024-02-05 01-53-41.png)

确保当前运行的内核版本号与 DKMS 模块匹配



##### SecureBoot 阻止了驱动加载

如果启用了 Secure Boot，系统可能会阻止未签名的驱动加载。NVIDIA 驱动需要在 Secure Boot 禁用或正确配置的环境中加载。

检查 Secure Boot

```bash
mokutil --sb-state 
```

重启时进入 BIOS 修改或终端禁用

```bash
sudo mokutil --disable-validation
```

注意，Secure Boot 不一定要禁用，正确配置不影响 NVIDIA 驱动加载。



#### 重新安装

卸载已有的 NVIDIA 显卡驱动

重启时，按住`shift`访问 GRUB 菜单，选择`Advanced options for Ubuntu`，进入指定内核的`Recovery Mode`，选择`root`进入命令行，输入以下代码卸载已安装的驱动

```bash
sudo apt-get --purge remove nvidia*
sudo apt-get --purge remove "*nvidia*"
sudo apt autoremove
```

确认 Nouveau 已禁用

重新通过图形化界面下载（建议）

确认 Secure Boot 状态已被禁用

*[ 如未禁用 Secure Boot*

*设置 Secure Boot 的密码*

*重启后进入蓝屏*

*选择 Enroll MOK 输入 Secure Boot 的密码*

*选择 reboot ]*

重新启动后确认内核版本与驱动版本匹配

确认 NVIDIA 驱动已加载，如未加载则手动加载

检查显卡驱动

```bash
nvidia-smi
```

![Screenshot from 2024-02-05 01-51-10](.\img\ubuntu nvidia driver installation\Screenshot from 2024-02-05 01-51-10.png)



#### 总结

