FROM ros:kinetic

SHELL ["/bin/bash", "-c"]

# dependencies of launch files for demos
# - p2os to understand robot messages
# - tf for frames (laser)
# - gmapping and navigation for SLAM
# - git to download custom ROS packages
RUN apt-get update && apt-get install -y \
        ros-kinetic-p2os-msgs \
        ros-kinetic-tf2-ros \
        ros-kinetic-gmapping \
        ros-kinetic-navigation \
        git

# install custom ROS packages (to understand its messages)
RUN mkdir -p /catkin_ws/src
WORKDIR /catkin_ws/src
# tele-operation of daisy
ADD https://api.github.com/repos/tuw-cpsg/general-ros-modules/compare/master...HEAD /dev/null
RUN git clone https://github.com/tuw-cpsg/general-ros-modules.git

# build custom ROS packages
WORKDIR /catkin_ws
RUN source /opt/ros/kinetic/setup.bash && catkin_make

# initialize ROS (master uri, environments, etc.)
COPY docker-entrypoint.sh /
ENTRYPOINT ["/docker-entrypoint.sh"]

# default command
CMD ["bash"]
