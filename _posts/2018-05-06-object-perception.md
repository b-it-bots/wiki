---
title: Object Perception
tags:
  - perception
---

# Object Perception

## Scene Segmentation \(mcr\_scene\_segmentation\)

* `roslaunch mcr_scene_segmentation scene_segmentation.launch`
* Components:
  * workspace finder: Finds planes of \(usually horizontal\) workspaces
    * `workspace_finder.launch`: set of PCL nodelets for plane segmentation
    * `workspace_finder_node`: combines PolygonStamped and ModelCoefficients messages into PlanarPolygon \(representation of planar workspace\)
  * `tabletop_cloud_accumulator_node`: Segments points above given PlanarPolygon and accumulates points from multiple frames \(should be separated into two components\)
  * `tabletop_cloud_clusterer_node`: Clusters given pointcloud based on Euclidean distance
  * `bounding_box_maker_node`: visualizes bounding box of clusters
* Important parameters:
  * `workspace_constraints.yaml`:
    * transform: filter\_limit\_max: points further than this from the camera are filtered out
    * voxel\_filter: filter\_limit\_min/max: range in z-axis of base\_link in which points are considered
    * passthrough\_x: filter\_limit\_min/max: range in x-axis of base\_link in which points are considered
    * planar\_segmentation: axis: Planes whose normals are along this axis are considered \(within angular\_threshold\)
  * `tabletop_cloud_accumulator_node` \(scene\_segmentation.launch\)
    * `min_height`, `max_height`: range of height above the planar polygon from which points are segmented
    * `accumulate_clouds`: number of frames to accumulate before segmenting points
  * `tabletop_cloud_clusterer_node` \(scene\_segmentation.launch\)
    * `cluster_tolerance`: minimum distance between clusters
    * `min_distance_to_polygon`: clusters whose centroid is closer than this threshold to the polygon are discarded \(in case only half the object is within the polygon\)
    * `min_cluster_size`, `max_cluster_size`: minimum and maxmimum number of points allowed in a cluster \(smaller and larger clusters are rejected\)
* Triggers
  * `rostopic pub /mcr_perception/mux_pointcloud/event_in std_msgs/String e_trigger` \(switches pointcloud multiplexer from empty topic to camera pointcloud or vice versa\). This will trigger all components in `workspace_finder.launch`
  * `rostopic pub /mcr_perception/mux_pointcloud/select std_msgs/String /arm_cam3d/depth_registered/points` \(select exact topic which the mux will publish\)
  * `rostopic pub /mcr_perception/workspace_finder/event_in std_msgs/String e_trigger` \(trigger workspace finder node to publish PlanarPolygon message \(on the topic /mcr\_perception/workspace\_finder/polygon\)

## Object Detection \(mcr\_object\_detection\)

* `roslaunch mcr_object_detection object_detection.launch` \(includes scene\_segmentation.launch\)
* Uses `scene_segmentation.launch` to find horizontal planes and clusters of object candidates
* \(ros/scripts/\)`object_detector`: This is a state machine that calls the different components in `scene_segmentation` and calls `object_recognizer` service
  * publishes `ObjectList` message
  * calculates pose of object as centroid of cluster, and orientation along three principal axes
  * publishes tf of all objects
* Triggers
  * `rostopic pub /mcr_perception/object_detector/event_in std_msgs/String e_trigger` \(triggers object detector and publishes object list \(on topic `/mcr_perception/object_detector/object_list`\)

## Object Recognition \(mcr\_object\_recognition\_mean\_circle\)

* `roslaunch mcr_object_recognition_mean_circle object_recognition.launch` \(includes object\_detection.launch\)
* Provides a service to classify objects using a previously trained svm classifier

## Tools

### Collecting object pointcloud clusters

* `roslaunch mcr_perception_tools collect_object_pointclouds.launch`
* Place one object on a workspace
* roscd mcr\_perception\_tools/ros/scripts && ./collect\_object\_pointclouds --dataset  --confirm-every  
  * example: ./collect\_object\_pointclouds --dataset atwork\_objects --confirm-every 5 S40\_40\_B
* Confirm the dataset and object name are correct
* Confirm the detected workspace is correct
* Check rviz to see if the detected cluster is correct
* Move the object to a different pose, then confirm the object cluster is correct
* Repeat until you have ~100 samples of the object, then repeat for different objects

### Training SVM classifier

* roscd mcr\_object\_recognition\_mean\_circle/ros/tools && ./train\_classifier.py --dataset  --output 
  * example: ./train\_classifier.py --dataset atwork\_objects --output atwork\_objects
* classifier is saved in common/config/atwork\_objects
* specify classifier name \(atwork\_objects\) in object\_recognition.launch

