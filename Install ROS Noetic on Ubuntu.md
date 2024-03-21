## Install ROS Noetic on Ubuntu

*for ubuntu 20.04 lts*

*official documentation: http://wiki.ros.org/noetic/Installation/Ubuntu*

### Configure Ubuntu repositories

```bash
sudo add-apt-repository restricted
sudo add-apt-repository universe
sudo add-apt-repository multiverse
```

```bash
sudo apt update
```

### Set up sources.list

```bash
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
```

### Set up keys

```bash
sudo apt install curl # if you haven't already installed curl
curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
```

### Installation

```bash
sudo apt update
```

### Environment setup

```bash
source /opt/ros/noetic/setup.bash
```

```bash
echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

### Install dependencies

```bash
sudo apt install python3-rosdep python3-rosinstall python3-rosinstall-generator python3-wstool build-essential
```

### Initialize rosdep

```bash
sudo rosdep init
rosdep update
```

### Check

```bash
rosversion -d
```

### Test

```bash
source /opt/ros/noetic/setup.bash
```

```bash
roscore
```

```bash
rosrun turtlesim turtlesim_node
```

```bash
rosrun turtlesim turtle_teleop_key
```

### Errors

```bash
Preparing to unpack .../python3-catkin-pkg-modules_0.4.24-1_all.deb ...
Unpacking python3-catkin-pkg-modules (0.4.24-1) ...
dpkg: error processing archive /var/cache/apt/archives/python3-catkin-pkg-modules_x.x.x-x_all.deb (--unpack):
 trying to overwrite '/usr/lib/python3/dist-packages/catkin_pkg/__init__.py', which is also in package python3-catkin-pkg x.x.x-x
...
Errors were encountered while processing:
 /var/cache/apt/archives/python3-catkin-pkg-modules_x.x.x-x_all.deb
 /var/cache/apt/archives/python3-rospkg-modules_x.x.x-x_all.deb
 /var/cache/apt/archives/python3-rosdistro-modules_x.x.x-x_all.deb
 E: Sub-process /usr/bin/dpkg returned an error code (1)
```

The error message clearly says that it is trying to overwrite a few files because there is a package that has already created those files. In simple words, the package was supposed to place one of its files in `/usr/lib/python3/`, but those files were already there, so it started throwing error messages.

Actually, those packages are placed in `/var/cache/apt/archives/`. This is `apt`'s cache directory, where it downloads files and waits for `dpkg` to install them. As they are stored in `apt`'s cache, every time using `apt`, `dpkg` starts processing those packages.

Use `dpkg -i --force-overwrite <file>` to make it safer.

```bash
dpkg -i --force-overwrite /var/cache/apt/archives/python3-catkin-pkg-modules_x.x.x-x_all.deb
dpkg -i --force-overwrite /var/cache/apt/archives/python3-rospkg-modules_x.x.x-x_all.deb
dpkg -i --force-overwrite /var/cache/apt/archives/python3-rosdistro-modules_x.x.x-x_all.deb
```

```bash
sudo apt -f install
```

