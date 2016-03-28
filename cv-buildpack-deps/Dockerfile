FROM kaixhin/cuda:latest
MAINTAINER Victor Melo <victorhcmelo@gmail.com>

# Built using PyImageSearch guide: 
# http://www.pyimagesearch.com/2015/06/22/install-opencv-3-0-and-python-2-7-on-ubuntu/
# Thank you, Adrian Rosebrock (twitter.com/pyimagesearch)

# Set CUDA_ROOT
ENV CUDA_ROOT /usr/local/cuda/bin

# Install dependencies
RUN \ 
    # step 1
    apt-get update && apt-get upgrade -y && \

    # step 2 
    apt-get install build-essential cmake git pkg-config -y && \

    # step 3
    apt-get install libjpeg8-dev libtiff4-dev libjasper-dev libpng12-dev -y && \

    # step 4
    apt-get install libgtk2.0-dev -y && \

    # step 5
    apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev -y && \

    # step 6
    apt-get install libatlas-base-dev gfortran -y && \
    
    # add support to HDF5 (available on OpenCV 3.1.0)
    apt-get install libhdf5-dev -y && \

    # step 7
    # RUN wget https://bootstrap.pypa.io/get-pip.py
    # RUN python get-pip.py
    apt-get install python-pip -y && \
    pip install --upgrade pip && \

    # step 8
    pip install virtualenv virtualenvwrapper && \
    rm -rf ~/.cache/pip && \

    # step 9 
    apt-get install python2.7-dev -y && \
    pip install numpy && \
    # RUN python -c 'import numpy as np; print np.__version__'

    apt-get autoclean && apt-get clean && \

    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

