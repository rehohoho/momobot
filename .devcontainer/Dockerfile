# Note to maximize caching, leave the more frequently rebuilt portions toward the end
# For dev, use host volumes, relax consistency for speed
FROM osrf/ros:melodic-desktop

# install ros package, fix network time protocol (remove clock skew error), update bashrc
RUN apt-get update && apt-get install -y \
    nano tmux ntp \
    python-pygame \
    ros-melodic-robot-localization \
    ros-melodic-rosserial-python \
    ros-melodic-imu-filter-madgwick \
    python3-catkin-tools
    # rm -rf /var/lib/apt/lists/* && \

RUN echo "source /opt/ros/${ROS_DISTRO}/setup.bash" >> ~/.bashrc

# Only define which port the image should listen to, not actually port forwarding
EXPOSE 9090

# These commands copy your files into the specified directory in the image
# and set that as the working location
WORKDIR /usr/src/momobot
COPY ../ /usr/src/momobot

RUN touch /usr/src/momobot*
  # cat /usr/src/momobot/.devcontainer/append_bashrc >> ~/.bashrc

# Build ROS files
# RUN /bin/bash -c ". /opt/ros/melodic/setup.bash && cd /usr/src/momobot/momobot_ws && catkin build"

# This command runs your application, comment out this line to compile only
# CMD ["ros2", "launch", "demo_nodes_cpp", "talker_listener.launch.py"]
LABEL Name=momobot Version=0.0.1
