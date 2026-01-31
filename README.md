# RESCUE-DT
Robotic Environments for Search and resCUE using Digital Twins

**To cite this work:**
De Nóbrega Bullón, K., Almenara Reyes, O., Bravo Arrabal, J., Vázquez Martín, R., Fernández Lozano, J.J., García Cerezo, A. 2026. 
Towards digital twins in field robotics: ROS2-Unity3D integration for search and rescue applications. 
Submitted to Revista Iberoamericana de Automática e Informatica Industrial. 2026.

Some **videos** can be seen at https://www.youtube.com/playlist?list=PLzGHhHCD9XWRZUDRAvq-ftrLqUgAzODbC. 

## 1. Introduction
This project is part of an ongoing research line in digital twin technologies for disaster robotics, specifically focusing on Search and Rescue (SAR) applications. It expands on a previous Unity 3D + ROS 2 simulation of the J8 Rover by introducing new capabilities that bring the system closer to a real-time digital twin. The simulation enables testing and development of control and perception algorithms in a controlled setting before implementation on the physical J8 robot, but also enables the real-time virtual representation of data received from the physical environment via ROS 2, enhancing the situational awareness and realism of the simulation.

Technologies used:

* **ROS2 Humble**: Robotics framework for creating nodes and inter-node communication.
* **Unity**: Game engine used to create the virtual environment and simulate the robot's physics.
* **ROS-TCP-Connector**: Bridge for communication between ROS2 and Unity.

## 2. Environment Setup
Prerequisites:
* **Operating system**: Linux (Ubuntu 22.04 recommended)
* **ROS2 Humble**: Follow the official installation instructions: https://docs.ros.org/en/humble/Installation.html
* **Unity**: Download and install the version used in the project (2022.3.44f1). It can run on Ubuntu or Windows. https://unity.com/es/download
* **ROS2 package installation**:

 * Clone the ROS2 workspace:

```
git clone https://github.com/Robotics-Mechatronics-UMA/LAENTIEC-J8_ros2_unity.git
cd LAENTIEC-J8_ros2_unity/src 
```
 * Compile the packages:
```
colcon build
```
* **Unity Configuration**:
* Download the folder containing the project: Unity-ROS2-Project. **IMPORTANT**: This repository is being updated. In the meantime, please refer to https://github.com/Kmdnb/TFG_KDN_UnityROS2 for the Unity files.

* Open the Unity project:
 * From Unity Hub - Select "Open project": Once the editor has started, you will see a welcome screen. Look for and select the "Open project" option.
 * Navigate to the folder where the project is downloaded: A file explorer window will open. Navigate to the location where the Unity-ROS2-Project folder is located.
 * Select the folder and open: Once you have located the project folder, select it and click the "Open" button.

## 3. ROS2-Unity Communication
Communication between ROS2 and Unity is established through the ROS-TCP-Connector. ROS2 nodes publish and subscribe to topics to send and receive data. In Unity, scripts handle reading and writing topic data. Follow the steps in the official ROS-TCP-Connector documentation to install and run this package in Unity and ROS2: https://github.com/Unity-Technologies/Unity-Robotics-Hub/tree/main This package includes the URDF Importer for Unity.  

## 4. Unity Preparation
Once the project is open and the ROS-TCP-Connector package is configured, follow these steps to increase the terrain texture resolution:

* Go to Assets >3D Meshes > Textures, and click on the TerrainTexture image.
* Then, change the settings accordingly. Recommended values:
 * Aniso Level = 16
 * Max Size = 16384
 * Compression = High Quality.

## 5. Project Execution
**Starting ROS2**:
* Open several terminals.
* Source the ROS2 setup:
```
source ~/ros2_ws/install/setup.bash
```
* Establish a connection with Unity through ROS-TCP-Connector.
```
ros2 run ros_tcp_endpoint default_server_endpoint --ros-args -p ROS_IP:= [YOUR_IP]
```
* Run the nodes in different terminals:
```
ros2 run teleop_twist_keyboard teleop_twist_keyboard #Teleoperate
ros2 run camera_subscriber camera_subscriber #Camera view of the ARGO J8
ros2 run lidar_subscriber lidar_subscriber #Lidar response
ros2 run fixposition_pkg gps_subscriber #GPS response
ros2 run fixposition_pkg imu_subscriber #IMU response
ros2 run fixposition_pkg odometry_subscriber #Odometry response
```
**Starting Unity**:

* Run the project scene in Unity

* Verifying the connection:

ROS2: Check that sensor readings are consistent.

Unity: Verify that data is being received and processed correctly in Unity.

At this point, you have a working simulator of the environment and ARGO J8 UGV, with teleoperation capabilities through ROS 2.

## 6. Extended functionalities

6.1 Download & Replace Assets
Download this repository and replace the Assets folder of the original Unity project with the one provided here.

# Example command (adjust the path to your project)
cp -r ./TFG-OAR-ROS2-Unity/Assets ./TFG_KDN_UnityROS2/Assets
3.2 Additional Elements
This folder includes:

Complete models for the UAV, the J8 rover, and human characters.
All scripts used for control, simulation, and agent logic.
Materials and textures for realistic terrain rendering.
3.3 Key Scripts Included
The following scripts are included as major innovations in this project:

CameraSwitch – Switch between different Unity cameras using the C key.
CenitalDroneCamera – Provides a top-down view of the UAV.
DronePoseSubscriber – Main UAV script that subscribes to GPS data via ROS 2 and moves the drone accordingly.
FlyCamera – Free camera control script.
FollowCameraDrone – Third-person follow view of the UAV.
HumanFollower – Controls SAR agents, showing real-time GPS position and helmet battery percentage.
J8TrayectoryFollower – Main Rover script to show real-time position and odometry from physical sensors.
4. New Agents & Features
4.1 UAV (Multirotor Drone)
Based on a six-rotor platform inspired by the DJI Matrice 600.
Controlled via ROS 2 topic with GPS data from a real system.
Follows waypoints in real-time simulation.
4.2 Human SAR Agents
Human characters representing first responders.
Each carries a GPS-enabled helmet that shares position and battery info with Unity via ROS 2.
5. Project Execution
To run the full system:

Start your ROS 2 environment in your Linux terminal. (Launch the nodes that publish GPS and sensor data if you are using rosbag).

Start the ROS-TCP-Endpoint server.

Launch the Unity project with the replaced Assets folder.

✅ Verify Unity–ROS 2 communication is working.

In Unity, go to Robotics → ROS Settings and configure the IP and port of the ROS 2 machine.
Also, in the Hierarchy panel, select the ROS_Connector GameObject and in the Inspector configure the same IP and port.
6. Multimedia
The multimedia folder includes:

Screenshots from the Unity simulation.
Real photos from field testing with the Rover J8.
Comparative visuals between simulation and real-world deployment.


## 6. Multimedia
This section includes an image of the robot and the simulated terrain, as well as a video summarizing the simulation's operation.
<img width="594" height="1863" alt="image" src="https://github.com/user-attachments/assets/1464a2a4-7ffe-4533-ab06-0f34b70e1ae5" />
