FROM ubuntu:14.04
MAINTAINER Victor Melo <victorhcmelo@gmail.com>

# Built using PyImageSearch guide: 
# http://www.pyimagesearch.com/2015/06/22/install-opencv-3-0-and-python-2-7-on-ubuntu/
# Thank you, Adrian Rosebrock (twitter.com/pyimagesearch)

# Install dependencies
RUN \ 
    # step 1
    apt-get -qq update && apt-get -qq upgrade -y && \

    # step 2 
    apt-get -qq install build-essential cmake git pkg-config -y && \

    # step 3
    apt-get -qq install libjpeg8-dev libtiff4-dev libjasper-dev libpng12-dev -y && \

    # step 4
    apt-get -qq install libgtk2.0-dev -y && \

    # step 5
    apt-get -qq install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev -y && \

    # step 6
    apt-get -qq install libatlas-base-dev gfortran -y && \
    
    # add support to HDF5 (available on OpenCV 3.1.0)
    apt-get -qq install libhdf5-dev -y && \

    # step 7
    # RUN wget https://bootstrap.pypa.io/get-pip.py
    # RUN python get-pip.py
    apt-get -qq install python3-pip -y && \
    pip3 install --upgrade pip && \

    # step 8
    pip3 install virtualenv virtualenvwrapper && \
    rm -rf ~/.cache/pip && \

    # step 9 
    apt-get -qq install python3.4-dev -y && \
    pip3 install numpy && \
    # RUN python -c 'import numpy as np; print np.__version__'

    apt-get autoclean && apt-get clean && \

    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


# Download OpenCV 3.1.0 and install
# step 10 
RUN \
    cd ~ && \
    git clone https://github.com/Itseez/opencv.git && \
    cd opencv && \
    pwd && \
    git checkout 3.1.0 && \

    cd ~ && \
    git clone https://github.com/Itseez/opencv_contrib.git && \
    cd opencv_contrib && \
    git checkout 3.1.0 && \

    cd /root/opencv && \
    mkdir build && \
    cd build && \
    cmake -D CMAKE_BUILD_TYPE=RELEASE \
        -D CMAKE_INSTALL_PREFIX=/usr/local \
        -D INSTALL_C_EXAMPLES=OFF \
        -D INSTALL_PYTHON_EXAMPLES=ON \
        -D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib/modules \
        -D BUILD_EXAMPLES=ON .. && \

    cd ~/opencv/build && \
    make -j $(nproc) && \
    make install && \
    ldconfig && \

    ls ~/opencv/build/lib/cv2.cpython-34m.so && \  # DEBUG
    cp ~/opencv/build/lib/cv2.cpython-34m.so /usr/local/lib/python3.4/dist-packages/cv2.so && \

    # clean opencv repos
    rm -rf ~/opencv && rm -rf ~/opencv_contrib

    # step 11
    # RUN cd ~/.virtualenvs/cv/lib/python2.7/site-packages/
    # RUN ln -s /usr/local/lib/python2.7/site-packages/cv2.so cv2.so

