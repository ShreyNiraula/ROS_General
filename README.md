# ROBOT_STATE_PUBLISHER

- ref:
	- [http://wiki.ros.org/robot_state_publisher]


- for publishing the state of robot to tf
- state means the 3d poses (xyzrpy) of link to tf
- which are being obtained from the state of joints (usually from the joint state publisher)
- and from the robot_description parameters in URDF file.

- simply taken as library/node, but easy to work as node.


- for more on subsribed topics, parameters see from 2.1 in the URL [http://wiki.ros.org/robot_state_publisher]



## use of robot state publisher in own robot 
- ref: [http://wiki.ros.org/robot_state_publisher/Tutorials/Using%20the%20robot%20state%20publisher%20on%20your%20own%20robot]


### Basic idea
- either as node or library
- here focused as __node__

1. Two criteria beforehead:
	- we need to run urdf xml robot description loaded on the Parameter Server.
	- we need source that gives the state of joint so that computation is carried out to publish the 3D pose of links ie, we need the joint positions as a __sensor_msgs/JointState__

2. create a launch file
	- in this launch file, be sure to load the urdf into parameter server as:
		- ```  <param name="my_robot_description" textfile="$(find mypackage)/urdf/robotmodel.xml"/> ```

	- be sure to get value from joint state publisher any how either directly or by remapping to suitable topic.

### complete launch file example:::
```
<launch>
   <!-- Load the urdf into the parameter server. -->
   <param name="my_robot_description" textfile="$(find mypackage)/urdf/robotmodel.xml"/>
    
   <node pkg="robot_state_publisher" type="robot_state_publisher" name="rob_st_pub" >
      <remap from="robot_description" to="my_robot_description" />
      <remap from="joint_states" to="different_joint_states" />
    </node>
  </launch>
```






