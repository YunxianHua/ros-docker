# docker build -t ros-kinetic -f ./kinetic-ros/Dockerfile . 
FROM ubuntu:16.04

ENV ROS_DISTRO=kinetic

# install lsb-release
RUN apt-get update && apt install lsb-release -y

# source list
RUN sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'

# set key
RUN apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654

# install ros kinetic base
RUN apt-get update && apt install ros-kinetic-ros-base -y

COPY ./kinetic-ros/python/__init__.py /usr/lib/python2.7/dist-packages/rosdistro/__init__.py
COPY ./kinetic-ros/python/rep3.py /usr/lib/python2.7/dist-packages/rosdep2/rep3.py
COPY ./kinetic-ros/python/sources_list.py /usr/lib/python2.7/dist-packages/rosdep2/sources_list.py
COPY ./rosdistro /root/rosdistro

RUN rosdep init && rosdep update --include-eol-distros

RUN echo "source /opt/ros/$ROS_DISTRO/setup.bash" >> ~/.bashrc

