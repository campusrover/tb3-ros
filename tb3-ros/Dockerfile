FROM dorowu/ubuntu-desktop-lxde-vnc:focal

# BASE IMAGE CUSTOMIZATIONS -----------------------------------------------------------------------

ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8

ENV ROS_DISTRO noetic

RUN wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | sudo apt-key add -

# Install system dependencies
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
    nano \
    micro \
    wget \
    curl \
    tar \
    make \
    git \
    curl \
    openssh-server \
    iptables \
    iproute2 \
    iputils-ping \
    netcat


# ROS melodic support
RUN echo "deb http://packages.ros.org/ros/ubuntu focal main" > /etc/apt/sources.list.d/ros1-latest.list
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
    ros-noetic-desktop-full
    
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
    build-essential \
    python3-rosdep \
    python3-rosinstall \
    python3-rosinstall-generator \
    python3-wstool \
    python3-vcstools \
    ros-noetic-rqt \
    ros-noetic-rqt* \
    ros-noetic-rviz \
    ros-noetic-catkin \
    ros-noetic-teleop-twist-keyboard \
    ros-noetic-image-transport \
    ros-noetic-compressed-image-transport \
    ros-noetic-camera-info-manager \
    ros-noetic-diagnostics \
    ros-noetic-tf \
    ros-noetic-tf2

 # Tailscale VPN support
RUN mkdir -p /my_ros_data/tailscale
RUN curl -vsLo tailscale.tar.gz "https://pkgs.tailscale.com/stable/tailscale_1.2.10_amd64.tgz" && \
    tar xvf tailscale.tar.gz && \
    mv "tailscale_1.2.10_amd64/tailscaled" /usr/bin && \
   mv "tailscale_1.2.10_amd64/tailscale" /usr/bin

RUN chmod +x /usr/bin/tailscale
RUN chmod +x /usr/bin/tailscaled


# Code-server
RUN mkdir /code-server && \
    curl -fL https://github.com/cdr/code-server/releases/download/v3.6.1/code-server-3.6.1-linux-amd64.tar.gz \
    | tar xvz --strip-components=1 -C /code-server


# Workspace and catkin_ws setup
WORKDIR /my_ros_data/
RUN echo "source /opt/ros/noetic/setup.bash" >> .bashrc && \
    mkdir -p catkin_ws/src/ && \
    rosdep init && \
    rosdep update
    
WORKDIR /my_ros_data/catkin_ws 
RUN /bin/bash -c "source /opt/ros/noetic/setup.bash && catkin_make -DPYTHON_EXECUTABLE=/usr/bin/python3 && source devel/setup.bash"


# COURSE SPECIFIC CONFIGURATIONS ------------------------------------------------------------------
WORKDIR /my_ros_data

ENV TB3_MODEL=burger \
    TURTLEBOT3_MODEL=burger \
    HOME=/my_ros_data \
    NAME_CATKIN_WORKSPACE=/my_ros_data/catkin_ws

# Copy needed files
ADD files/rootfs/.bashrc .
ADD files/rootfs/.jwmrc /entry/
COPY files/sshd/sshd_config /etc/ssh/
COPY files/nginx/default /etc/nginx/sites-enabled/
COPY files/supervisor/supervisord.conf /etc/supervisor/conf.d/

RUN mkdir -p /my_ros_data/.config/code-server
COPY files/code-server/config.yaml /my_ros_data/.config/code-server/config.yaml


WORKDIR /my_ros_data/catkin_ws/src
RUN git clone https://github.com/ROBOTIS-GIT/turtlebot3_msgs.git
RUN git clone https://github.com/ROBOTIS-GIT/turtlebot3.git
RUN git clone https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git
RUN git clone https://github.com/campusrover/prrexamples.git
RUN git clone https://github.com/campusrover/gpg_bran4.git

WORKDIR /my_ros_data
RUN git clone https://github.com/campusrover/rosutils.git
WORKDIR /my_ros_data/rosutils
RUN cat bashrc_template.bash > /my_ros_data/.bashrc

RUN ln -s /my_ros_data/rosutils/bru.py /usr/local/bin/bru && chmod +x bru.py


COPY ./entrypoint.sh /entry/
RUN chmod +x /entry/entrypoint.sh

# Override entrypoint of base image
ENTRYPOINT []
CMD ["bash", "-c", "/entry/entrypoint.sh"]
