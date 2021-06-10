# Application of NCP on Jackal Robot
* Cyber-Physical Systems Design and Application Final Project
* Bowen Feng and Sonia Yuxiao Lai

## Overview

## Requirements
* [Clearpath Jackal](https://clearpathrobotics.com/jackal-small-unmanned-ground-vehicle/#:~:text=Jackal%20is%20a%20small%2C%20fast,%2Dthe%2Dbox%20autonomous%20capability.)
* [Intel&reg;RealSense&trade; Depth Camera D435i](https://www.intelrealsense.com/depth-camera-d435i/)
* [TensorFlow](https://www.tensorflow.org/)
* [OpenCV](https://opencv.org/#)
* [Jackal_ROS_Noetic_Bringup](https://github.com/dinvincible98/Jackal_ROS_Noetic_Bringup)
* [cv_bridge](http://wiki.ros.org/cv_bridge)
* [realsense2_camera](http://wiki.ros.org/realsense2_camera)

## Bringup Jackal
1. ssh into Jackal
    a. ```source setup_jackal.bash```
    b. ```roslaunch jackal_noetic_bringup velodyne.launch```
    c. ```roslaunch jackal_neotic_bringup slam_toolbox_jakcal.launch```
2. on PC
    a. ```source setup_laptop.bash```
    b. ```roslaunch jackal_noetic_bringup slam_toolbox_pc.launch```

## Prepare Data for Velodyne
Run the following command while using slam_toolbox in rviz or running a rosbag 
```
rosrun ncp read_data
```  
This will store a npy file including laser scan data, linear and angular velocities in current directory. 



## Prepare Data for Line Following
Run the following commands to drive Jackal on a pathway    
```
roslaunch realsense2_camera rs_camera.launch 
rosrun teleop_twist_keyboard teleop_twist_keyboard.py
rosrun ncp collect_image
```  
This will store images from the realsense camera with angular velocity in folder `/images` with file name in format `<ang_vel>_image_<rnd_str>.png`.  

## Train Model
The following files in `/notes` contain information on how to train the models:
* read_bag_linear.ipynb
* read_bag_angular.ipynb
* line_follow_files.ipynb

## Load Model
Edit load_model to load model and rung Jackal using either velodyne or camera 
```
rosrun ncp load_model
```  


