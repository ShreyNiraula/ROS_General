# Frames and TF

## Frame
- linear motion
	- right hand rule
	- index =x , middle =y, thumb = z

- angular motion
	- right curl
	- thumb= z axis, so curl is rotation on z , with anticlockwise direction = +ve





## TF
- for keeping track of many frames in system
- many frames, world, base, head etc. 

- tf keeps changes of these frames as per time
- ie, how it has changed during time elaspse of like 1secc.

- tells how pose of object in head changed with respect to base

- tells the current estimated pose of base in world map.




## Visualization
- to visualize tf, we may use ``` rosrun tf view_frames ``` 
