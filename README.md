This repository contains a simulation developed for the **Challenge for participation in the Mobile Robotics Research Project - VeRLab 2025.1** 🤖. The goal of the challenge was to create a ROS Gazebo simulation of the **Scout Mini**, a mobile robot from **AgileX**, equipped with either a **LiDAR sensor** or an **RGB camera** 📷.

In this implementation, both sensors were added to the Scout Mini 🔧and both are configured to be connected and operating in Rivz after the simulation is launched
. Additionally, a room with walls and a table was created 🏠 to simulate the VeRLab and provide a better visualization of the sensors’ functionality in **RViz** 🔍.

To facilitate interaction with the simulation, the **teleop_twist_keyboard** was configured, allowing manual control of the robot 🎮.

The package was developed to operate with **ROS 2 Jazzy**, using the **Gazebo Harmonic** simulator on **Ubuntu 24.04** 🖥️. Below, you will find all the necessary instructions to run the simulation ⬇️.

### Usage for the Scout Mini (ROS2 Jazzy + Ubuntu 24.04 + Gazebo Harmonic)
The following steps assume you're using Ubuntu 24.04

### Download ROS2 Jazzy 
## Set locale
Make sure you have a locale which supports UTF-8. If you are in a minimal environment (such as a docker container), the locale may be something minimal like POSIX. We test with the following settings. However, it should be fine if you’re using a different UTF-8 supported locale.
```bash
locale  # check for UTF-8

sudo apt update && sudo apt install locales
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8

locale  # verify settings
```
## Enable required repositories
You will need to add the ROS 2 apt repository to your system.

First ensure that the Ubuntu Universe repository is enabled.
```bash
sudo apt install software-properties-common
sudo add-apt-repository universe
```
Now add the ROS 2 GPG key with apt.
```bash
sudo apt update && sudo apt install curl -y
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg11
```
Then add the repository to your sources list.
```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```
## Install development tools (optional)
If you are going to build ROS packages or otherwise do development, you can also install the development tools:
```bash
sudo apt update && sudo apt install ros-dev-tools
```
## Install ROS 2
Update your apt repository caches after setting up the repositories.
```bash
sudo apt update
```
ROS 2 packages are built on frequently updated Ubuntu systems. It is always recommended that you ensure your system is up to date before installing new packages.
```bash
sudo apt upgrade
```
Desktop Install (Recommended): ROS, RViz, demos, tutorials.
```bash
sudo apt install ros-jazzy-desktop
```
ROS-Base Install (Bare Bones): Communication libraries, message packages, command line tools. No GUI tools
```bash
sudo apt install ros-jazzy-ros-base
```
Automatic environment setup
```bash
echo "source /opt/ros/jazzy/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

### Download Gazebo Harmonic
First install some necessary tools:
```bash
sudo apt-get update
sudo apt-get install curl lsb-release gnupg
```
Then install Gazebo Harmonic:
```bash
sudo curl https://packages.osrfoundation.org/gazebo.gpg --output /usr/share/keyrings/pkgs-osrf-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/pkgs-osrf-archive-keyring.gpg] http://packages.osrfoundation.org/gazebo/ubuntu-stable $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/gazebo-stable.list > /dev/null
sudo apt-get update
sudo apt-get install gz-harmonic
```

### Aditional necessary packages
To correctly build and run the simulation, you will need to install the following packages

xacro (used to process URDF files in ROS 2)
```bash
sudo apt install ros-jazzy-xacro
```
ros_gz_bridge (bridges the gap between ROS 2 and Gazebo)
```bash
sudo apt install ros-jazzy-ros-gz-bridge
```
ros_gz_image (integrate image communication between ROS 2 and the Gazebo simulator via the ros_gz_bridge)
```bash
sudo apt install ros-jazzy-ros-gz-image
```
ros_gz_sim (allows you to control and simulate robots within the Gazebo environment)
```bash
sudo apt install ros-jazzy-ros-gz-sim
```
nav2_commom (contains essential components and common utilities for the robot navigation system in ROS 2)
```bash
sudo apt install ros-jazzy-nav2-common
```
Colcon (build tool used in ROS 2)
```bash
sudo apt install python3-colcon-core python3-colcon-common-extensions
```
ament_cmake (
CMake build system extension used in ROS 2 to ease package development and building)
```bash
sudo apt install ros-jazzy-ament-cmake  
```

### Running the simulation
Download the repository:
```bash
git clone https://github.com/ThiagoHSAl/desafio_ros2_verlab_2025.1.git
```
```bash
cd desafio_ros2_verlab_2025.1
```
Building the package: 
```bash
colcon build
```
Source the built packages:
```bash
. install/setup.bash
```
Launch the simulation environment:
```bash
ros2 launch scout_gazebo_sim scout_mini_empty_world.launch.py
```
In another terminal launch the keyborad to move the robot:
```bash
ros2 run teleop_twist_keyboard teleop_twist_keyboard
```
### **teleop_twist_keyboard Explanation**

The **teleop_twist_keyboard** node takes keyboard inputs and publishes them as **Twist** or **TwistStamped** messages, which are commonly used to control robot movement in ROS. This package works best with a **US keyboard layout**.

#### **Moving Around**:
- **u**: Move the robot diagonally up-left.
- **i**: Move the robot forward (increase linear speed along the x-axis).
- **o**: Move the robot diagonally up-right.
- **j**: Move the robot left (decrease linear speed along the x-axis).
- **k**: Stop the robot (no movement).
- **l**: Move the robot right (increase linear speed along the x-axis).
- **m**: Move the robot diagonally down-left.
- **, (comma)**: Move the robot backward (decrease linear speed along the x-axis).
- **. (period)**: Move the robot diagonally down-right.

#### **Holonomic Mode (for strafing, sideways movement)**:
Hold down the **Shift** key to enter **Holonomic mode**, which allows strafing (sideways movement):
- **U**: Move the robot diagonally up-left.
- **I**: Move the robot forward (increase linear speed along the x-axis).
- **O**: Move the robot diagonally up-right.
- **J**: Move the robot left (decrease linear speed along the x-axis).
- **K**: Stop the robot (no movement).
- **L**: Move the robot right (increase linear speed along the x-axis).
- **M**: Move the robot diagonally down-left.
- **< (less than)**: Move the robot backward (decrease linear speed along the x-axis).
- **> (greater than)**: Move the robot diagonally down-right.

#### **Additional Controls**:
- **t**: Move the robot up (along the z-axis).
- **b**: Move the robot down (along the z-axis).
- **anything else**: Stop the robot immediately.
- **q**: Increase the maximum speed of the robot by 10%.
- **z**: Decrease the maximum speed of the robot by 10%.
- **w**: Increase only the linear speed by 10%.
- **x**: Decrease only the linear speed by 10%.
- **e**: Increase only the angular speed by 10%.
- **c**: Decrease only the angular speed by 10%.

#### **Exiting the Program**:
- **CTRL-C**: Quit the program.

### Parameters of <i>scout_mini_empty_world.launch.py</i>:
- <b>use_rviz</b>: if you want to launch rviz2 or not, default <i>true</i>.
- <b>rviz_config_file</b>: name of the configuration file for RVIz2, defautl <i>scout_mini.rviz</i>.
- <b>use_sim_time</b>: use simulation time or not, default <i>true</i>.
- <b>x_pose</b>: x coordinate of the robot at the start, default <i>0.0</i>.
- <b>x_pose</b>: x coordinate of the robot at the start, default <i>0.0</i>.
- <b>yaw angle</b>: yaw angle of the robot at the start, default <i>3.14</i>.
- <b>world_name</b>: name of the used world, the world must be in the world folder, default <i>empty.world</i>.
