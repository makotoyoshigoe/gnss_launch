# gnss_launch

## Setup GNSS
### Clone and build this package
```
mkdir -p ~/gnss_ws/src
cd ~/gnss_ws/src
git clone git@github.com:makotoyoshigoe/gnss_launch.git
cd ../ && colcon build --symlink-install
source install/setup.bash
```
### Install ublox package
```
sudo apt update
sudo apt install ros-$ROS-DISTRO-ublox
```
### Launch GNSS
```
sudo chmod 666 /dev/ttyACM0
ros2 launch gnss_launch ublox_gps_node-zed_f9r.launch.py
```