### Usage for the Scout Mini (ROS2 Jazzy + Ubuntu 24.04 + Gazebo Harmonic)
Building the package:
```bash
    mkdir src
```
```bash
    cd src
```
```bash
    git clone https://github.com/ThiagoHSAl/desafio_ros2_verlab_2025.1.git
``` 
```bash
    cd ..
```
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
Launch the keyborad to move the robot:
```bash
    ros2 run teleop_twist_keyboard teleop_twist_keyboard --ros-args --remap /cmd_vel:=/scout_mini/cmd_vel
```
### Parameters of <i>scout_mini_empty_world.launch.py</i>:
- <b>use_rviz</b>: if you want to launch rviz2 or not, default <i>true</i>.
- <b>rviz_config_file</b>: name of the configuration file for RVIz2, defautl <i>scout_mini.rviz</i>.
- <b>use_sim_time</b>: use simulation time or not, default <i>true</i>.
- <b>x_pose</b>: x coordinate of the robot at the start, default <i>0.0</i>.
- <b>x_pose</b>: x coordinate of the robot at the start, default <i>0.0</i>.
- <b>yaw angle</b>: yaw angle of the robot at the start, default <i>3.14</i>.
- <b>world_name</b>: name of the used world, the world must be in the world folder, default <i>empty.world</i>.
