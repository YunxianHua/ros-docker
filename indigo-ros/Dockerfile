# docker build -t ros-indigo -f ./indigo-ros/Dockerfile . 
FROM ubuntu:14.04

ENV ROS_DISTRO=indigo

# install lsb-release
RUN apt-get update && apt install lsb-release -y

# source list
RUN sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'

# set key
RUN apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116

# install ros indigo base
RUN apt-get update && apt install ros-indigo-ros-base -y --force-yes

COPY ./indigo-ros/python/__init__.py /usr/lib/python2.7/dist-packages/rosdistro/__init__.py
COPY ./indigo-ros/python/rep3.py /usr/lib/python2.7/dist-packages/rosdep2/rep3.py
COPY ./indigo-ros/python/sources_list.py /usr/lib/python2.7/dist-packages/rosdep2/sources_list.py
COPY ./rosdistro /root/rosdistro

RUN rosdep init && rosdep update --rosdistro $ROS_DISTRO

RUN echo "source /opt/ros/$ROS_DISTRO/setup.bash" >> ~/.bashrc

