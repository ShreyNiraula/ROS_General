# JOINT STATE PUBLISHER

- ref:
	- [http://wiki.ros.org/joint_state_publisher]

- publishes about the state of the joint
- in the form of sensor_msgs/JointState
- based on parameters from param server, it publishes the Jointstate msgs for non-fixed joints such as continuous, 
revolute, floating, prismatic etc.


- can take the values from possible sources of:
	- GUI input
	- from subscribed other jointstate msgs
	- the value of another joint
	- default value that can be zero or some given value

## GUI
- previously we had to set __use_gui__ to __True__
- now, gui functionality is in its own package: __joint_state_publisher_gui__
- use of old way although supported not recommended
- also,for packages transitioning before this change, __joint_state_publisher_gui__ should be added as an __<exec_depend>__ to package.xml and launch files should be updated to launch __joint_state_publisher_gui__ instead of using __joint_state_publisher__ with __use_gui__ parameter.


## Dependency
- one joint can be made to depend on another.
- eg: with one rotation of pulley, another needs to be turned 3 times, then 
	- ``` joint_D: {parent: joint_A, factor: 3 } ``` means jointD depends on jointA as 3 times factor, which can be 3 times rotation or something like that. 

- more example:
	- joint_F: {parent: joint_C, factor: -1 } // opposite acting types of dependency


## Default values
- usually zero(0)
- but with specific defined value, we define within as
	- ``` 
		zeros:
  		  joint_A: 1.57
  		  joint_B: 0.785
	  ```


## More...

- the package can be used more in conjuction with __robot_state_publisher__
- url: [http://wiki.ros.org/robot_state_publisher]
 





