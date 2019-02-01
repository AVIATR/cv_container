############################################################
# Dockerfile to build a raspbian container with OpenCV 4.x
############################################################

#Set up the prerequisites
FROM raspbian/stretch
MAINTAINER Ender Tekin <etekin@wisc.edu>
ENV DEBIAN_FRONTEND noninteractive
ENV SOURCE_DIR /tmp/rtmp_server
ENV OPENCV_REPOSITORY https://github.com/opencv/opencv.git
WORKDIR ${SOURCE_DIR}
RUN apt-get update && \
    apt-get install -y -q build-essential cmake pkg-config && \
    apt-get install -y -q libavformat-dev libavcodec-dev libavfilter-dev libswscale-dev libv4l-dev && \
    apt-get install -y -q libjpeg-dev libpng-dev libtiff-dev libeigen3-dev libgtk-3-dev && \
    apt-get install -y -q libatlas-base-dev gfortran libcanberra-gtk* && \
    apt-get autoremove && \
    apt-get clean
    
#Install Opencv - see https://www.pyimagesearch.com/2018/09/26/install-opencv-4-on-your-raspberry-pi/
RUN mkdir ${SOURCE_DIR}/opencv && \
    cd ${SOURCE_DIR}/opencv && \
    git clone --depth 1 OPENCV_REPOSITORY && \
    mkdir build && \
    cd build && \
    cmake -D CMAKE_BUILD_TYPE=RELEASE \
	-D CMAKE_INSTALL_PREFIX=/usr/local \
    -D ENABLE_CXX11=ON \
    -D WITH_GSTREAMER=OFF \
    -D BUILD_opencv_java=OFF \
    -D BUILD_opencv_python=OFF \
    -D WITH_CUDA=OFF \
    .. && \
    make -j$(nproc) && \
    make install 

CMD ["/bin/bash"]
