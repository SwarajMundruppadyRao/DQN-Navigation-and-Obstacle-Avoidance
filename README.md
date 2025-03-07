# DQN-Navigation-and-Obstacle-Avoidance

This repository contains the submission for ENPM690 Project - Autonomous Navigation and Obstacle Avoidance using Deep Q-Network

To get more information about the model, parameters and the results, please refer to the project report: [REPORT](https://github.com/suhasnagaraj99/DQN-Navigation-and-Obstacle-Avoidance/blob/main/Group24_ENPM690_Project_Report.pdf)

![Video GIF](https://github.com/suhasnagaraj99/DQN-Navigation-and-Obstacle-Avoidance/blob/main/690.gif)

## Repository Structure
- **enpm690_dqn**: Package for autonomous navigation and obstacle avoidance using Deep Q-Network.
- **turtlebot3_msgs**: Package for defining ros messages used by turtlebot3
- **turtlebot3_simulations**: Package for simulating turtlebot3 on gazebo
- **models**: Folder storing the trained DQN models. 

## Prerequisites
- Before running the code, ensure that you have the following installed:
  - ROS2 (Version: Humble)
  - Gazebo
  - Python 3.10
  - Pytorch 2.2.2
  - matplotlib
  - pandas
  - gpu access and nvidia cuda toolkit
  - colcon build tool (`sudo apt install python3-colcon-common-extensions`)
  - turtlebot3_description package (`sudo apt-get install ros-humble-turtlebot3-description`)

## Setup Instructions

1. **Create a Workspace**:
   ```bash
   mkdir -p ~/ros2_ws/src
   cd ~/ros2_ws/src
   ```
2. **Copy Packages**:
   - Paste the packages, from the zip folder, inside the src of the ros workspace
   
3. **Download Models**:
   - Download the pretrained model models required for simulation from [HERE](https://drive.google.com/drive/folders/1i67uRLK7YeFl8OiVD6KFPxqoXSdHe5AQ?usp=sharing).
   - Paste this model folder inside the src of ros workspace.
     
4. **Build and Source the Packages**:
   ```bash
   cd ~/ros2_ws
   colcon build
   source install/setup.bash
   source /usr/share/gazebo/setup.sh
   ```
5. **Inside `.bashrc`, set paths for the workspace and plugins used**:
  - First oprn `.bashrc`
   ```bash
   nano ~/.bashrc
   ```
  - Then paste the following lines inside the bashrc
   ```bash
   WORKSPACE_DIR=~/ros2_ws
   export DRLNAV_BASE_PATH=$WORKSPACE_DIR
   source $WORKSPACE_DIR/install/setup.bash
   export GAZEBO_MODEL_PATH=$GAZEBO_MODEL_PATH:$WORKSPACE_DIR/src/turtlebot3_simulations/turtlebot3_gazebo/models
   export TURTLEBOT3_MODEL=burger
   export GAZEBO_PLUGIN_PATH=$GAZEBO_PLUGIN_PATH:$WORKSPACE_DIR/src/turtlebot3_simulations/turtlebot3_gazebo/models/turtlebot3_drl_world/obstacle_plugin/lib
   ```
  - Source the `.bashrc`
   ```bash
   source ~/.bashrc
   ```

## Running the Simulation

1. **Launch Turtlebot3 in Gazebo**:
   ```bash
   ros2 launch turtlebot3_gazebo turtlebot3_drl_stage4.launch.py
   ```
  
3. **Run the dqn environment node**:
   ```bash
   ros2 run enpm690_dqn dqn_envi
   ```
   
3. **Run the dqn gazebo node**:
   ```bash
   ros2 run enpm690_dqn dqn_gazebo
   ```

4. **Run the main dqn node for testing the model**:
   ```bash
   ros2 run enpm690_dqn dqn_test "dqn_2_stage_4" 2600
   ```
   
4. **Results**:
   - The robot tried to avoid obstacles and reach the goal to maximize its rewards

## Acknowledgments

I would like to express my gratitude to the author of the [turtlebot3_drlnav](https://github.com/tomasvr/turtlebot3_drlnav) repository. This project relies on the code and resources provided in that repository, and I appreciate the work that went into developing it. Credit for the base code goes to the original author. Thank you for your contributions!
