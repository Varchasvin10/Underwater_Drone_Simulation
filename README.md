# Underwater Drone Simulation on Ubuntu 18.04 with ROS Melodic and Gazebo

Welcome to the Underwater Drone Simulation project! This README provides a guide to setting up and running an underwater drone simulation using Ubuntu 18.04, ROS Melodic, and Gazebo. This simulation environment allows you to test and develop algorithms for underwater robotics in a virtual setting.

## Prerequisites

Before setting up the simulation, ensure you have the following prerequisites installed:

1. **Ubuntu 18.04**: The operating system used for this setup.
2. **ROS Melodic**: The Robot Operating System (ROS) version for this project.
3. **Gazebo**: The simulation tool used for creating and running the virtual environment.

### Installing ROS Melodic

1. **Setup your sources.list**:
   ```bash
   sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu bionic main" > /etc/apt/sources.list.d/ros-latest.list'
   ```

2. **Setup your keys**:
   ```bash
   sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key '421C365BD9FF1F71'
   ```

3. **Install ROS Melodic**:
   ```bash
   sudo apt update
   sudo apt install ros-melodic-desktop-full
   ```

4. **Initialize rosdep**:
   ```bash
   sudo rosdep init
   rosdep update
   ```

5. **Set up your environment**:
   ```bash
   echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc
   source ~/.bashrc
   ```

6. **Install rosinstall**:
   ```bash
   sudo apt install python-rosinstall python-rosinstall-generator python-wstool build-essential
   ```

### Installing Gazebo

Gazebo is included in the ROS Melodic installation, but you can install the latest version if needed:

1. **Install Gazebo**:
   ```bash
   sudo apt install gazebo9 libgazebo9-dev
   ```

2. **Install Gazebo ROS packages**:
   ```bash
   sudo apt install ros-melodic-gazebo-ros ros-melodic-gazebo-ros-pkgs
   ```

## Setting Up the Simulation

1. **Create a ROS workspace**:
   ```bash
   mkdir -p ~/catkin_ws/src
   cd ~/catkin_ws/
   catkin_make
   source devel/setup.bash
   ```

2. **Clone the underwater drone simulation repository**:
   ```bash
   cd ~/catkin_ws/src
   git clone <repository-url>
   ```

3. **Install dependencies**:
   If the simulation package has dependencies, install them using:
   ```bash
   cd ~/catkin_ws
   rosdep install --from-paths src --ignore-src -r -y
   ```

4. **Build the workspace**:
   ```bash
   cd ~/catkin_ws
   catkin_make
   ```

5. **Source the workspace**:
   ```bash
   source devel/setup.bash
   ```

## Running the Simulation

1. **Launch Gazebo with the underwater world**:
   ```bash
   roslaunch uuv_gazebo_worlds ocean_waves.launch
   ```

2. **Launch the Drone**:
   ```bash
   roslaunch uuv_descriptions upload_rexrov.launch mode:=default x:=0 y:=0 z:=-20 namespace:=rexrov
   ```
3. **Use Teleop Keys with the cascaded PID controller**
   ```bash
   roslaunch uuv_control_cascaded_pid key_board_velocity.launch model_name:=rexrov
   ```

## Troubleshooting

- **Gazebo crashes or fails to start**: Ensure that all dependencies are correctly installed and the ROS workspace is built. Check for error messages in the terminal for clues.
- **Missing ROS packages or libraries**: Use `rosdep` to install missing dependencies.
- **Build issues**: Verify that all source files and configurations are correct.

## Contributing

If you would like to contribute to this project, please fork the repository, make your changes, and submit a pull request. Make sure to include relevant documentation and test your changes thoroughly.

## License

This project is licensed under the [MIT License](LICENSE). See the LICENSE file for details.


Happy simulating!

---

Feel free to modify this template to better suit your specific project details and requirements.
