=== Run Project ====================================================================
A. After first time run project, each time development: 
1. Open Ubuntu
2. cd /root/ros2_ws/src/my_bot

3. Source the ROS 2 environment:
source /opt/ros/humble/setup.bash
3. Navigate to your workspace:
cd /root/ros2_ws

4. Source your workspace:
source install/setup.bash

5. Run the launch file

5.1 To run the file
ros2 launch my_bot rsp.launch.py use_sim_time:=true
ros2 launch my_bot rsp_sim.launch.py
(Previous:ros2 launch my_bot rsp.launch.py)

5.2 To run gazebo
ros2 launch gazebo_ros gazebo.launch.py
ros2 run gazebo_ros spawn_entity.py -topic robot_description -entity my_bot


A.1 Run The left wheel right wheel
ros2 run joint_state_publisher_gui joint_state_publisher_gui

B. Run Rviz2
cd /root/ros2_ws/src/my_bot
source /opt/ros/humble/setup.bash
cd /root/ros2_ws
source install/setup.bash
rviz2 -d src/my_bot/config/view_bot.rviz
(Previous: rviz2)

C. After chagne the code:
colcon build --packages-select my_bot (previous: colcon build --symlink-install)
ros2 launch my_bot rsp.launch.py

=== First time rviz2 ===============================================================
Left Panel Fixed Frame: base_link
Left bottom Add button
Choose: TF
Click TF on the left panel
Check "Show Names" checkbox
Left bottom Add button
Choose: Robot Model
Click Robot Model on the left panel
Decription Tocpic type: /robot_description

-- After added left right joint --
sudo apt install ros-humble-joint-state-publisher-gui
ros2 run joint_state_publisher_gui joint_state_publisher_gui

First time run project:
0. Open your WSL2 terminal.
1. Navigate to your project directory:
cd /mnt/c/Users/noel_chung/Desktop/SA\ Related/my_bot
2. Create a ROS 2 workspace (if not already done):
mkdir -p ~/ros2_ws/src
ln -s /mnt/c/Users/noel_chung/Desktop/SA\ Related/my_bot ~/ros2_ws/src/my_bot
3. Build the project:
cd ~/ros2_ws
colcon build
4. Source the workspace:
source ~/ros2_ws/install/setup.bash
5. Run the project
ros2 launch my_bot rsp.launch.py

=== /Run Project ===================================================================
=== Install ROS ====================================================================
Install ROS for Ubuntu 22.04.3 LTS (GNU/Linux 5.15.153.1-microsoft-standard-WSL2 x86_64)
I. Set locale:
1. sudo apt update && sudo apt install locales
2. sudo locale-gen en_US en_US.UTF-8
3. sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
4. export LANG=en_US.UTF-8
II. Setup Sources:
1. sudo apt install software-properties-common
2. sudo add-apt-repository universe
3. sudo apt update && sudo apt install curl -y
4. echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
III.Install ROS 2 packages:
1. sudo apt update
2. sudo apt install ros-humble-desktop -y
IV. Source the setup script (you'll need to do this every time you open a new terminal, or add it to your ~/.bashrc file):
1. source /opt/ros/humble/setup.bash
V. Install development tools and ROS tools:
1. sudo apt install python3-rosdep python3-rosinstall python3-rosinstall-generator python3-wstool build-essential -y
VI. Initialize rosdep:
1. sudo rosdep init
2. rosdep update
VII. Test the installation: Open two terminal windows. In the first one, run:
1. source /opt/ros/humble/setup.bash
2. ros2 run demo_nodes_cpp talker
3. In the second terminal, run:
source /opt/ros/humble/setup.bash
4. ros2 run demo_nodes_py listener
Outpt: can see first termindal publishing hello world and 2nd publishing hello world
VIII. Checking
1. Make sure your CMAKE_PREFIX_PATH includes the ROS 2 installation:
echo $CMAKE_PREFIX_PATH
2. If it's empty or doesn't include the ROS 2 path, set it:
export CMAKE_PREFIX_PATH=$CMAKE_PREFIX_PATH:/op
=== /Install ROS ===================================================================
=== Install Colcon =================================================================
Colcon is the build tool used for ROS 2 projects.
1. First, make sure your system is up to date:
sudo apt update && sudo apt upgrade -y
2. Install colcon:
sudo apt install python3-colcon-common-extensions
=== /Install Colcon ================================================================
=== Install Xacro ==================================================================
1. sudo apt-get update
2. sudo apt-get install ros-humble-xacro
=== /Install Xacro =================================================================
=== /Install rvis2 =================================================================
A. Follow below:
https://github.com/ros2/rviz?tab=readme-ov-file

If have problem follow below:
sudo apt update
sudo apt purge --yes ros-humble-ament-cmake-vendor-package
sudo apt install --yes ros-humble-ament-cmake-vendor-package
dpkg -L ros-humble-ament-cmake-vendor-package | grep Findament_cmake_vendor_package.cmake
cd ~/rviz2_ws/build 
rm -rf *
cd ..
source /opt/ros/humble/setup.bash
colcon build --merge-install 

B. After complete robot_core.xacro, save rviz to the workspace
File > Save config as> root > ros2_ws > src > my_bot > config > File Nmae: view_bot.rviz

-- Install Gazebo
sudo apt install ros-humble-gazebo-ros-pkgs   (as I use ubuntu cannnot use ros-foxy-gazebo-ros-pkgs)
sudo apt install ros-humble-gazebo-ros

exampl: Open seesaw example: gazebo /usr/share/gazebo-11/worlds/seesaw.world
=== /Install rvis2 =================================================================
=== Box Design =====================================================================
300mm*300mm*150mm
the box is 300mm width 300mm long, 150mm high = (American) 1foot by one foot by haldf a foot => 0.3 0.3 0.15

base_link = center of wheel in the bottom, got X,Y,Z => to front, Y is left or right, z is up
chassie_joint = just behind the center of the two drive wheels in the bottom => xyz=-0.1 0 0

original center of the chessie, x = 0.3/2 = 0.15, z = 0.15/2 = 0.075
to make the visual left in the back in the bottom xyz=0.15 0 0.075

x=froward
y=left
z=up
=== /Box Design ====================================================================