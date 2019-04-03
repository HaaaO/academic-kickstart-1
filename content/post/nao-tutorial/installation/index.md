+++
title = "NAO Dev Tutorial: Installation"
subtitle = "Installing NAOqi SDK and configure NAO with ROS :rocket:"

date = 2019-01-23T00:00:00
lastmod = 2019-04-02T00:00:00
draft = false

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = ["admin"]

tags = ["Academic"]
summary = "Installing NAOqi SDK and configure NAO with ROS."

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["deep-learning"]` references 
#   `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
# projects = ["nao-tutorial/installation"]

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

## Installing the SDK
1. Make sure you have the following installed
    - [Python 2.7](https://www.python.org/download/releases/2.7/)
    - [CMake](https://cmake.org/) version 2.8.3 or higher
    
1. Download the following from [Aldebaran Community](https://community.aldebaran.com/en/resources/software) website \(*you need to register an account in order to download the files*\)
    - **pynaoqi-python-2.7-naoqi-2.1.2.x-linux64.tar.gz**
    - **naoqi-sdk-2.1.2.x-linux64.tar.gz**
    - \[optional\] **choregraphe-suite-\[2.1.4 or 2.1.2\].x-linux64.tar**
    
1. Execute the following command and replace **2.1.2.x** with the version you downloaded

    Unzip the tar files
    ```bash
    $ mkdir ~/naoqi
    $ tar xzf <path to NAOqi C++ SDK>/naoqi-sdk-2.1.2.x-linux64.tar -C ~/naoqi/naoqi-sdk-2.1.2-linux64
    $ tar xzf <path to NAOqi Python SDK>/pynaoqi-python2.7-2.1.2-linux64.tar -C ~/naoqi/naoqi-sdk-2.1.2-linux64
    ```
    
    Check the installation by executing NAOqi
    ```bash
    $ ~/naoqi/naoqi-sdk-2.1.2.17-linux64/naoqi
    ```
    You should see output similiar to
    ```
    Starting NAOqi version 2.1.2.17
    .
    .
    .
    NAOqi is ready...
    ```
    
    Press **CTRL-C** to exit

    Now we need to add **NAOqi SDK** to system variables. Add the following lines at the end of **~/.bashrc**
    ```bash
    $ export PYTHONPATH=~/naoqi/pynaoqi-python2.7-2.1.2-linux64:$PYTHONPATH
    $ export AL_DIR=~/naoqi/naoqi-sdk-2.1.2-linux64
    $ export AL_DIR_SIM=~/naoqi/naoqi-sdk-2.1.2-linux64
    ```
    
    Execute `source ~/.bashrc` to apply the changes

    Verify *in python console*
    ```python
    import naoqi
    ```
    if correctly installed, there should be no error



## Install ROS
- See [Official ROS Installation Tutorial](http://wiki.ros.org/kinetic/Installation)

## Install **NAO package** for ROS
- Install the packages needed
  - *replace kinetic to your ROS version if needed*
    
    ```bash
    $ sudo apt-get install ros-kinetic-driver-base ros-kinetic-move-base-msgs \
    ros-kinetic-octomap ros-kinetic-octomap-msgs ros-kinetic-humanoid-msgs \
    ros-kinetic-humanoid-nav-msgs ros-kinetic-camera-info-manager \
    ros-kinetic-camera-info-manager-py
    ```

- Install the main package
  ```bash
  $ sudo apt-get install ros-kinetic-nao-robot
  ```

- Install packages for robot control
  ```bash
  $ sudo apt-get install ros-kinetic-nao-bringup ros-kinetic-naoqi-pose \
  ros-kinetic-nao-interaction ros-kinetic-nao-moveit-config \
  ros-kinetic-naoqi-driver ros-kinetic-naoqi-driver-py \
  ros-kinetic-naoqi-sensors-py ros-kinetic-nao-dcm-bringup \
  ros-kinetic-moveit
  ```

- Install packages for simulation

  *Notice: to install nao_meshes package, you need to agree the policy*
  ```bash
  $ sudo apt-get install ros-kinetic-rospack ros-kinetic-nao-meshes
  ```

## Next: [Getting Started](/post/nao-tutorial/getting-started/)

### Reference
- [Python SDK Install Guide](http://doc.aldebaran.com/2-1/dev/python/install_guide.html)
- [C++ SDK Installation](http://doc.aldebaran.com/2-1/dev/cpp/install_guide.html)
- [Installation of ROS for usage with or on a NAO robot](http://wiki.ros.org/nao/Tutorials/Installation)
