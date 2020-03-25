 # Memo for ROS (Robotics Operating System) 


- To run the master (need to do this first):  `roscore`
- To run a node: `rosrun <Package Name> <Node Name>`
    - Node: is an executive file of a package
    - Package: includes nodes, libraries, CMakeList, etc. 
- To list all nodes: `rosnode list`
- To list all topics: `rostopic list` 
- To list all services: `rosservice list` 
- To get topic info: `rostopic info /<TOPIC NAME>`
- To get the details of message type `rosmsg show <Package Name>/<Message Definition Name>`
- To view and edit ROS file: `rosed <Package Name>/<Message Definition Name>`
- To look a topic's messages in real time: `rostopic echo /<Topic Name>` 

- To crate Catkin Workspace - this contains all of the packages of a project. 
    - Create worskapce directory: `mkdir -p ~/catkin_ws/src` 
    - Move to src directory: `cd ~/catkin_ws/src` 
    - Initialize the workspace: `catkin_init_workspace`
    - Move to the top level directory: `cd ~/catkin_ws`
    - Build the workspace: `catkin_make`

- To clone a pakcage into a Catkin Workspace
    - Move to src directory: `cd ~/catkin_ws/src` 
    - Clone a package: `git clone <Repository Name> <Package Name>`
    - Move to the top level directory: `cd ~/catkin_ws`
    - Build the workspace: `catkin_make` 

- To launch a workspace (ROS with multiple nodes): 
    - Move to the top level directory: `cd ~/catkin_ws`
    - Build the workspace: `catkin_make` 
    - Source set up script: `source devel/setup.bash` 
    - Launch: `roslaunch <Package Name> <Launch file Name>`
        - Launch file (.launch) defines nodes to launch together

- To check missing dependencies: `rosdep check <Package Name>` 
- To install missing dependencies: `rosdep install -i <Package Name>`

- To create a package: 
    - Move to src directory: `cd ~/catkin_ws/src
    - Create a package: `catkin_create_pkg <Package Name>`

- Structure of Catkin package: 
    - scripts: Python executables
    - src: C++ source files
    - msg: custom message definitions
    - srv: service message definitions
    - include: headers/libraries (dependencies)
    - config: configuration files
    - launch: launch files (.launch) to run multiple nodes
 
 - Structure of Service file (.srv)
    - Divided by '---' line
    - Above the line is the definition of the request message
    - Below the line is the service response

 - To create a node for Python 
    - Move to `src/scripts` directory: `cd src/<Package Name>/scripts`
    - Create a script: `touch <Node Name>`
    - Change permission: `chmod u+x <Node Name>`
    - Add the node in .launch file

 - To publish a topic in Python 
    - `pub1 = rospy.Publisher("/topic_name", message_type, queue_size=size)`
        - Syncrhonous when `queue` is `None`, else asynchronous publishing
    - `pub1.publish(message)`

-  To subscribe a topic in Python 
    - `sub1 = rospy.Subscriber("/topic_name", message_type, callback_function)`

-  To use Services in Python - ROS Service allows request/response communication between nodes
    - `service = rospy.Service('service_name', serviceClassName, handler)`
        - handeer: is called when service messages come, then responde

-  To use a Service from another node in Python
    - `service_proxy = rospy.ServiceProxy('service_name', serviceClassName)` 
    - `msg = serviceClassNameRequest()`
    - `response = service_proxy(msg)`

-  To see camera image stream: `rqt_image_view /rgb_camera/image_raw` 
-  To find log file: `roscd log`  



 - References:
    - ROS wiki:  wiki.ros.org
    - ROS answers:  answers.ros.org/questions/
    - ROS Cheat Sheet: https://github.com/ros/cheatsheet/releases/download/0.0.1/ROScheatsheet_catkin.pdf
    - Gentle Introduction to ROS: https://cse.sc.edu/~jokane/agitr/ 
