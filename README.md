# FAST-LIO-to-Nav-2
Terminal1:  ros2 launch unitree_lidar_ros2 launch.py
Terminal2: ros2 launch fast_lio mapping.launch.py config_file:=unilidar_l2.yaml
Terminal3:  ros2 run pointcloud_to_laserscan pointcloud_to_laserscan_node   --ros-args   -r cloud_in:=/cloud_registered   -p target_frame:=unilidar_lidar   -p min_height:=-5.0   -p max_height:=5.0
 ros2 run pointcloud_to_laserscan pointcloud_to_laserscan_node   --ros-args   -r cloud_in:=/cloud_registered   -p target_frame:=unilidar_lidar   -p min_height:=-5.0   -p max_height:=5.0

ros2 run tf2_ros static_transform_publisher   0 0 0 0 0 0 1 body base_link
ros2 run tf2_ros static_transform_publisher   0 0 0 0 0 0 1 base_link unilidar_imu_initial
ros2 launch slam_toolbox online_async_launch.py slam_params_file:=/home/tanvi/LiDAR_ws/slam_params.yaml
ros2 run rqt_tf_tree rqt_tf_tree
 ros2 launch nav2_bringup navigation_launch.py   params_file:=/home/tanvi/LiDAR_ws/nav2_params.yaml   use_sim_time:=false

ros2 run rviz2 rviz2 -d /opt/ros/humble/share/nav2_bringup/rviz/nav2_default_view.rviz
ros2 topic echo /cmd_vel

put nav2 and slam params files in LiDAR_ws/
