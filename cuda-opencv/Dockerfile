FROM victorhcm/cv-buildpack-deps
MAINTAINER Victor Melo <victorhcmelo@gmail.com>

# Built using PyImageSearch guide: 
# http://www.pyimagesearch.com/2015/06/22/install-opencv-3-0-and-python-2-7-on-ubuntu/
# Thank you, Adrian Rosebrock (twitter.com/pyimagesearch)

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
        -D OPENCV_EXTRA_MODULES_PATH=/root/opencv_contrib/modules \
        -D BUILD_EXAMPLES=ON .. && \

    cd ~/opencv/build && \
    make -j $(nproc) && \
    make install && \
    ldconfig && \

    cp ~/opencv/build/lib/cv2.so /usr/local/lib/python2.7/dist-packages/

    # step 11
    # RUN cd ~/.virtualenvs/cv/lib/python2.7/site-packages/
    # RUN ln -s /usr/local/lib/python2.7/site-packages/cv2.so cv2.so

