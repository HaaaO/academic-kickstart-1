+++
title = "NAO Tutorial: Getting Started with NAO + ROS"
subtitle = "NAO setup with ROS :robot:"

date = 2019-01-23T00:00:00
lastmod = 2019-04-03T00:00:00
draft = false

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = ["admin"]

tags = ["Tutorial", "Robotics", "NAO", "ROS"]
summary = "This tutorial shows how to work with Physical NAO."

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["deep-learning"]` references 
#   `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
# projects = ["nao-tutorial/getting-started"]

# Featured image
# To use, add an image named `featured.jpg/png` to your project's folder. 
[image]
  # Caption (optional)
  caption = "Image credit: [**Unsplash**](https://unsplash.com/photos/CpkOjOcXdUY)"

  # Focal point (optional)
  # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
  focal_point = ""

  # Show image only in page previews?
  preview_only = false

# Set captions for image gallery.

[[gallery_item]]
album = "gallery"
image = "theme-default.png"
caption = "Default"

[[gallery_item]]
album = "gallery"
image = "theme-ocean.png"
caption = "Ocean"

[[gallery_item]]
album = "gallery"
image = "theme-forest.png"
caption = "Forest"

[[gallery_item]]
album = "gallery"
image = "theme-dark.png"
caption = "Dark"

[[gallery_item]]
album = "gallery"
image = "theme-apogee.png"
caption = "Apogee"

[[gallery_item]]
album = "gallery"
image = "theme-1950s.png"
caption = "1950s"

[[gallery_item]]
album = "gallery"
image = "theme-coffee-playfair.png"
caption = "Coffee theme with Playfair font"

[[gallery_item]]
album = "gallery"
image = "theme-cupcake.png"
caption = "Cupcake"

# Enable source code highlighting
highlight_languages = ["bash", "python"]

+++

This tutorial shows how to work with Physical NAO.

Make sure you have installed all the dependencies and configured **PYTHONPATH** system variable correctly

\**see [installation guide](/post/nao-tutorial/installation) for detail*

## Controlling Robot
1. Turn on the robot. See [this guide](http://doc.aldebaran.com/2-1/nao/getting_out_of_the_box.html) for detail
1. Start the robot bridge on your computer

    ```bash
    $ roslaunch nao_bringup nao_full_py.launch nao_ip:=<robot_ip> \
    roscore_ip:=<roscore_ip>
    ```
    
    This will start the robot's default configuration with the following publisher:
    - joint_states
    - tf
    - top camera
    - bottom camera
    - left sonar
    - right sonar
    - microphone

1. To visualize the robot, open **rviz**

    ```bash
    $ rosrun rviz rviz
    ```
    
    1. In top bar, go to `File->Open Config`
    1. navigate to `<your catkin workspace>/src/nao_robot/nao_description/config` and open the file with **.rviz** extension
        - make sure you have [nao_meshes](http://wiki.ros.org/nao_meshes) installed
    1. you should see something similar to the below screenshot
        ![NAO rviz](http://wiki.ros.org/nao/Tutorials/Getting-Started?action=AttachFile&do=get&target=NaoRviz.png)
1. Controlling the robot
    1. execute `rosnode list` to check if **/nao_walker** node is running
    1. To turn on the motors

        ```bash
        $ rosservice call /body_stiffness/enable "{}"
        ```
        To turn off the motors
        
        ```bash
        $ rosservice call /body_stiffness/disable "{}"
        ```
        
    1. once the motors are on, use the following command to move the robot in x-direction
    
        ```bash
        $ rostopic pub -1 /cmd_vel geometry_msgs/Twist \
        '{linear: {x: 1.0, y: 0.0, z: 0.0}, \
        angular: {x: 0.0, y: 0.0, z: 0.0}}'
        ```
        
        To stop the robot, run:
        ```bash
        $ rostopic pub -1 /cmd_vel geometry_msgs/Twist \
        '{linear: {x: 0.0, y: 0.0, z: 0.0}, \
        angular: {x: 0.0, y: 0.0, z: 0.0}}'
        ```

## Next: [NAOqi SDK Guide](/post/nao-tutorial/nao-sdk)

### Reference
- [Getting started with ROS for Nao, including NAOqi and rviz](http://wiki.ros.org/nao/Tutorials/Getting-Started)
- [nao_bringup](http://wiki.ros.org/nao_bringup)
