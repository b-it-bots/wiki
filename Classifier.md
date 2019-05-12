Getting the classifier from a data set
=======================================
### Pre-requisites

Install sklearn 0.17.1:
```sh
sudo pip install sklearn==0.17.1
```

Install Cython:
```sh
sudo pip install Cython
```

Clone the Python-pcl repository from the b-it-bots github page:
```sh
git clone git@github.com:b-it-bots/python-pcl.git
```

Go inside the python-pcl folder and run the following:
```sh
sudo python setup.py install
```

### Save the classifier

Go to the location of the 'train_classifier.py' file inside your catkin workspace and run that file with the given parameters:
```sh
cd *your catkin workspace*/src/mas_perception/mcr_object_recognition_mean_circle/ros/tools/
python train_classifier.py --dataset *add path to the folder with data to be trained here*
```

### Implement the classifier

Run the following to be able to use the classifier:
```sh
roslaunch mcr_object_recognition_mean_circle object_recognition.launch input_pointcloud_topic:=/camera/depth_registered/points target_frame:=base_link classifier:=classifier
```

To visualize your result on rviz, add the PointCloud2, Marker and MarkerArray feature in the rviz menu.

In the Marker tab, select the "/mcr_perception/scene_segmentation/bounding_boxes" topic.

In the MarkerArray tab, select the "/mcr_perception/scene_segmentation/labels" topic.

In the PointCloud2 tab, select "/mcr_perception/scene_segmentation/tabletop_clusters" topic.

Publish the message 'e_start':
```sh
rostopic pub /mcr_perception/scene_segmentation/event_in std_msgs/String "data: 'e_start'"
```

Publish the message 'e_add_cloud_start':
```sh
rostopic pub /mcr_perception/scene_segmentation/event_in std_msgs/String "data: 'e_add_cloud_start'"
```

Publish the message 'e_segment':
```sh
rostopic pub /mcr_perception/scene_segmentation/event_in std_msgs/String "data: 'e_segment'"
```
This last one will should enable the visualization of the classifier on rviz.
