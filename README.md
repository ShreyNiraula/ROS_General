# CLOCK	

- ref:
	- [http://wiki.ros.org/Clock]
	

- for when we need simulation time rather than wall-clock(pc clock)
- for purpose of accelerated, slowed or stepped control over system's percieved time

- eg cases are playing bag file, playing sensor data according to timestamp of sensor data // according to sensor calibrated timing, being simulated on the environment

## More Depth Knowledge
- simulation time is published on /clock
- we need to subscribe(listen) on that topic.
- usually ROS client libraries need to use the timeAPI for using simulation time.

- __Synchronization__ needed when multiple machines are involved, no direct implementation from ROS.

## Usuage
- need to set __/use_sim_time__ parameter must be set to __true__ before the node is initialized.
- If the __/use_sim_time__ parameter is set, the ROS Time API will return time=0 until it has received a value from the /clock topic. 
- Then, the time will only be updated on receipt of a message from the /clock topic, and will stay constant between updates.

- ie, in summary, once set, then time remains constant till the next update on /clock topic


## Clock server
- any node that publishes to /clock topic
- only one server should be there to publish to /clock

- eg: either rosbag play __--clock__ for simulation time or setting __/use_sim_time__ to __true__





