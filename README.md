# SOME COOL TRICKS IN ROS

## Echo to csv file
- we can rostopic echo the topic to csv file 
- `` rostopic echo -p /topic_name  > file.csv

- -p flag stores the echoed values in matlab friendly format suitable mainly for csv file format
- > sign is output stream syntax from scripting that writes (overwrites) on file
- if needed to append, use >> instead.


### More on topic
- if needed to store like only the header information, then do as ``` rostopic echo -p -n10 /topic_name/header > file.csv
- -n10 stores 1st 10 header info, (nx format, x for number of headers)
