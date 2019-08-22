This rospackage is modify from Mobilerobots, and I have gave a Chineses step for install the package in Pioner3-AT robots.

address: https://blog.csdn.net/crp997576280/article/details/98470571

# pioneer3at_pkg
Mobilerobots pioneer3at ROS package

## Environmental requirements
- Ubuntu 16.04 amd64
- ros-kinetic



## Installation and Configuration
### 1.Compile & Install [AriaCoda](https://github.com/reedhedges/AriaCoda)

- download source code & goto AriaCoda folder
  ```shell
  git clone https://github.com/QuartzYan/AriaCoda.git
  cd AriaCoda
  ```
- compile
  ```shell
  make
  ```
- install
  ```shell
  sudo make install
  ```

### 2.Compile & Install [pioneer3at ros pkg](https://github.com/QuartzYan/pioneer3at_pkg)
- download
  ```shell
  mkdir -p ~/ros_ws/src
  cd ~/ros_ws/src
  git clone https://github.com/QuartzYan/pioneer3at_pkg.git
  cd pioneer3at_pkg
  git submodule init
  git submodule update
  ```
- installation dependencies
  ```shell
  cd ~/ros_ws
  rosdep install --from-paths src --ignore-src --rosdistro=kinetic -y
  ```
- compile & environment setup
  ```shell
  catkin_make
  echo "source ~/ros_ws/devel/setup.bash" >> ~/.bashrc
  source ~/.bashrc
  ```

### 3.Creating the udev rule
- go to **pioneer3at_pkg/p3at_bringup/rules** folder, and copy *pioneer3at.rules* into the **/etc/udev/rules.d** folder.
  ```shell
  roscd p3at_bringup/rules
  sudo cp pioneer3at.rules /etc/udev/rules.d
  ```
  p.s:you can use **lsusb** command to query current serial number of the ftdi device.
- reload and restart the udev daemon
  ```shell
  sudo service udev reload
  sudo service udev restart
  ```


## How to use
### 1.start pioneer3at ros driver & rplidar driver
```shell
roslaunch p3at_bringup p3at_bringup.launch
```
then, you can view all of the topic
```shell
rostopic list
```

***Note: Before you do, you must first install [rplidar`s ros driver](https://github.com/QuartzYan/rplidar_ros)***

### 2.view robot modle
```shell
roslaunch p3at_description display.launch
```

### 3.mapping demo
```shell
roslaunch p3at_navigation gmapping_demo.launch
```
***Note: Before you do, you must first start pioneer3at ros driver and rplidar driver.***

When you are finished mapping, you can save it use:
```shell
rosrun map_serve map_save -f [map_name]
```

### 4.navigation demo
```shell
roslaunch p3at_navigation amcl_demo.launch
```
***Note: Before you do, you must first start pioneer3at ros driver and rplidar driver.***

You can revise ***amcl_demo.launch*** to load a different map.


