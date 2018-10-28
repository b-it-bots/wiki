How to use the RealSense2 camera
=================================

### Installation

Go to the intel-ros github page.
Clone the realsense repository in your catkin workspace inside src:
```sh
git clone git@github.com:intel-ros/realsense.git
```

### Camera Output

Run the following to get access to the camera:
```sh
roslaunch realsense2_camera rs_rgbd.launch
```

Open rviz to visualize the camera output.

### Configure camera output (OPTIONAL)

Run the following to open the rviz configuration window:
```sh
rosrun rqt_reconfigure rqt_reconfigure
```
You can also try to change the "octree_resolution" value:
```sh
cd *catkin workspace*/src/mas_perception/mcr_scene_segmentation/ros/config
gedit scene_segmentation_constraints.yaml
```

### Setup Base Frame

Run the following:
```sh
rosrun tf static_transform_publisher x y z roll pitch yaw base_link camera_link 100
```
where x, y, z are the distances and roll, pitch, yaw are the rotations from the base_link to the camera_link.

To visualize your frames in rzviz, add the TF feature in the rviz menu.

### Save Point Clouds

If it's your first time saving point clouds, you need to choose where you want to save them and enable data collection:
```sh
cd *catkin workspace*/src/mas_perception/mcr_scene_segmentation/ros/launch
gedit scene_segmentation.launch
```
Change the value of "dataset_collection" from "false" to "true".
Change value of "logdir" from "/temp/ to the path in your computer where you want to save the files.

Run the following to get access to the point clouds given by the camera:
```sh
roslaunch mcr_scene_segmentation scene_segmentation.launch input_pointcloud_topic:=/camera/depth_registered/points
```

Publish the message 'e-start':
```sh
rostopic pub /mcr_perception/scene_segmentation/event_in std_msgs/String "data: 'e_start'"
```

Publish the message 'e-add-cloud-start':
```sh
rostopic pub /mcr_perception/scene_segmentation/event_in std_msgs/String "data: 'e_add_cloud_start'"
```
This last one will save the current point cloud of the observed object in your system.

__BEWARE!!__ Sometimes the camera won't save the point cloud (don't worry, not your fault).
Just try a different position for the object until it works.

### Visualize Point Cloud

Run the following in the folder where you saved the point clouds:
```sh
pcl_viewer *.pcd file you want to open*
```
