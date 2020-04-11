# Image Transport Package

- ref:
	- [http://wiki.ros.org/image_transport]
	- [http://wiki.ros.org/image_transport/Tutorials]


- for transporting images in low bandwidth compressed format
- needs to be subsribed and published on images (accepts image format only)

## Abstraction
- abstract the complex image and video codec manipulation 
- for ease working with only sensor_msgs/Image message

## Dependency and Plugins
- default = raw image transport
- plugins available for more complicated trasport (eg compression)
- plugins not the part of ros dependency
- if plugins available in system, it auto uses that plugin without manual implication


## Usage
- similar to ROS Publisher and Subscriber
- but not only one node publication, many nodes when suitable transport available


_Instead of doing simple ros:: pub and ros::sub, we do as_
``` 
// instead of these....
ros::NodeHandle nh;
ros::Subscriber sub = nh.subscribe("in_image_topic", 1, imageCallback);
ros::Publisher pub = nh.advertise<sensor_msgs::Image>("out_image_topic", 1);

// we do as ....
ros::NodeHandle nh;
image_transport::ImageTransport it(nh);
image_transport::Subscriber sub = it.subscribe("in_image_base_topic", 1, imageCallback);
image_transport::Publisher pub = it.advertise("out_image_base_topic", 1);

// the above codes are parts of int main() while initiating nodes and creating pubs and subs 

```

-python not yet implemeted


## structure
- if /stereo/left/image, is default one, then when plugins for compression (say) available, image transport package auto publishes (along with default) the /stereo/left/image/compressed (this is mere example, there may not be such exact topics)



# Coding 

## Publisher code
- ref: [http://wiki.ros.org/image_transport/Tutorials/PublishingImages]

- simple demo where image is passed as argument which is accepted by openCV and then transfered to ROS sensor_msgs/Image format (with the help of CV_bridge)

- Using Image transport publisher Advertise function, 
	- we are going to be publishing images on the base topic "camera/image". 	 - Depending on whether more plugins are built, additional (per-plugin) topics derived from the base topic may also be advertised. 


## Subscriber Code
- ref: [http://wiki.ros.org/image_transport/Tutorials/SubscribingToImages]

- simple idea is that when openCV converts the image to ROS message format, then when these messages are available, callback function is called that converts it back to image and view on screen


## Running the Simple Image Publisher and Subscriber with Different Transports
- ref: [http://wiki.ros.org/image_transport/Tutorials/ExaminingImagePublisherSubscriber]

- with default nodes of those created above and run, we can perform the simple task as 

// image


- lets add new trasnport of compression

	- The compressed_image_transport package provides plugins for the "compressed" transport, which sends images over the wire in either JPEG- or PNG-compressed form. Notice that compressed_image_transport is not a dependency of your package; image_transport will automatically discover all transport plugins built in your ROS system.

	- Shut down your publisher node and restart it. If you list the published topics again, you should see a new one: 

	- ``` /camera/image/compressed [sensor_msgs/CompressedImage] 1 publisher ```

	- Now let's start up a new subscriber, this one using compressed transport. The key is that image_transport subscribers check the parameter ~image_transport for the name of a transport to use in place of "raw". Let's set this parameter and start a subscriber node with name "compressed_listener": 

	- ```  rosparam set /compressed_listener/image_transport compressed
	       rosrun image_transport_tutorial my_subscriber __name:=compressed_listener ```

	- the resultant rqt graph will be:

// images here....






