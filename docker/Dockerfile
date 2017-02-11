FROM osrf/ros:indigo-desktop-full

# install package dependencies
RUN apt-get update && apt-get install -y \
      python-catkin-tools \
      python-pip \
      python-scipy && \
    rm -rf /var/lib/apt/lists/*

# install python dependencies
RUN pip install \
      munkres \
      pykalman

# setup catkin workspace
ENV CATKIN_WS=/root/catkin_ws
RUN mkdir -p $CATKIN_WS/src
WORKDIR $CATKIN_WS/src

# clone project
RUN git clone https://github.com/angusleigh/leg_tracker.git

# replacing shell with bash for later docker build commands
RUN mv /bin/sh /bin/sh-old && \
    ln -s /bin/bash /bin/sh

# build ros package
WORKDIR $CATKIN_WS
ENV TERM xterm
ENV PYTHONIOENCODING UTF-8
RUN catkin config \
      --extend /opt/ros/$ROS_DISTRO \
      --cmake-args -DCMAKE_BUILD_TYPE=Release && \
    catkin build \
      --limit-status-rate 0.01 \
      --no-notify && \
    ldconfig

# conveniently add source to bashrc
RUN echo 'source "/opt/ros/${ROS_DISTRO}/setup.bash"\n\
    source "/root/catkin_ws/devel/setup.bash"\n'\
		>> ~/.bashrc
