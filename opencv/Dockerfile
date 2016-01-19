FROM ubuntu:14.04
MAINTAINER Victor Melo <victorhcmelo@gmail.com>

# Built using PyImageSearch guide: 
# http://www.pyimagesearch.com/2015/06/22/install-opencv-3-0-and-python-2-7-on-ubuntu/
# Thank you, Adrian Rosebrock (twitter.com/pyimagesearch)

# step 1
RUN apt-get update 
RUN apt-get upgrade -y

# step 2 
RUN apt-get install build-essential cmake git pkg-config -y

# step 3
RUN apt-get install libjpeg8-dev libtiff4-dev libjasper-dev libpng12-dev -y

# step 4
RUN apt-get install libgtk2.0-dev -y

# step 5
RUN apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev -y

# step 6
RUN apt-get install libatlas-base-dev gfortran -y

# step 7
# RUN wget https://bootstrap.pypa.io/get-pip.py
# RUN python get-pip.py
RUN apt-get install python-pip -y
RUN pip install --upgrade pip

# step 8
RUN pip install virtualenv virtualenvwrapper
RUN rm -rf ~/.cache/pip

# virtualenv and virtualenvwrapper
# export WORKON_HOME=RUNHOME/.virtualenvs
# source /usr/local/bin/virtualenvwrapper.sh
# mkvirtualenv cv

# step 9 
RUN apt-get install python2.7-dev -y
RUN pip install numpy
RUN python -c 'import numpy as np; print np.__version__'

# step 10 
RUN cd ~ \
    && git clone https://github.com/Itseez/opencv.git \
    && cd opencv \
    && pwd \
    && git checkout 3.1.0

RUN cd ~ \
    && git clone https://github.com/Itseez/opencv_contrib.git \
    && cd opencv_contrib \
    && git checkout 3.1.0

RUN cd /root/opencv \
    && mkdir build \
    && cd build \
    && cmake -D CMAKE_BUILD_TYPE=RELEASE \
        -D CMAKE_INSTALL_PREFIX=/usr/local \
        -D INSTALL_C_EXAMPLES=OFF \
        -D INSTALL_PYTHON_EXAMPLES=ON \
        -D OPENCV_EXTRA_MODULES_PATH=/root/opencv_contrib/modules \
        -D BUILD_EXAMPLES=OFF ..

RUN cd ~/opencv/build \
    && make -j4 \
    && make install \
    && ldconfig

# step 11
# RUN cd ~/.virtualenvs/cv/lib/python2.7/site-packages/
# RUN ln -s /usr/local/lib/python2.7/site-packages/cv2.so cv2.so


