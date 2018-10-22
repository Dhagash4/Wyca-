# Wyca-
This repo contains launch files that I used to create a map and instructions to build map in ROS Melodic 

Gmappping is currently not available for melodic but it will soon be availabe for melodic ROS environment.

The instructions to build map are:

1. Start roscore.

2. Then first set the parameter to use simulated time which can be setted by

   rosparam set use_sim_time true(This is important step for creating map with bag file)

3. Now you can tune the parameters available in Gmapping to create a map with better quality. I used the following

   rosparam set /slam_gmapping/xmax 10

   rosparam set /slam_gmapping/ymax 10

   rosparam set /slam_gmapping/ymin -10

   rosparam set /slam_gmapping/xmin -10
   
P.S:As I didnt knew about the sensors used and as the more the parameters more the computational load

4. Now start the gmapping node;

   rosrun gmapping slam_gmapping

5. After starting all this now start playing the bag file

   rosbag play --clock <filename.bag>

   This --clock is much needed to start the simulated time otherwise there will be erorrs

6. Now after starting this sit back till the bag file is completed and gmapping diagnostics stop printing it. Now the map is    made but you need to save it which we will do it by map_server package by running

   rosrun map_server map_saver -f <filename>
 
   Done this is how you can create a map with Rosbag file. 
-----------------------------------------------------------------------------------------------------------------------------

The other method I use to create map for my own robot is rtabmap_ros which is state of art Visual SLAM algorithm. To create a map using RTAB Map but the requirements are the robot should be equipped with Kinect and Lidar and rosbag should contain topics as /camera/rgb/image_color,/camera/depth/image,/camera/rgb/info with all the other topics like odom and tf.

1. Launch the default rtabmap launch file that is obtained with the package 

   roslaunch rtabmap.launch rtabmap_args:="--delete_db_on_start" 
   
   Also if the topic are not in the default state we can remap.
   
2. Now start the bag file 

   rosbag play <filename.bag>
 
3. Save the map from RTAB Map GUI

Hence made can be made by this also and its much simple as there is GUI and we can use it to tune parameters and also be cna save the whole recording in db then tune the parameters and see the changes in the map.
