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
5.After starting all this now start playing the bag file
rosbag play --clock <filename.bag>
This --clock is much needed to start the simulated time otherwise there will be eroors
6. Now after starting this sit back till the bag file is completed and gmapping diagnostics stop printing it. Now the map is made but you need to save it which we will do it by map_server package by running
rosrun map_server map_saver -f <filename>
 
Done this is how you can create a map with Rosbag file. 
