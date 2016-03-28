FROM victorhcm/cv-buildpack-deps
MAINTAINER Victor Melo <victorhcmelo@gmail.com>

# Built using PyImageSearch guide: 
# http://www.pyimagesearch.com/2015/06/22/install-opencv-3-0-and-python-2-7-on-ubuntu/
# Thank you, Adrian Rosebrock (twitter.com/pyimagesearch)

# Download OpenCV 3.1.0 and install
# step 10 

RUN \
    cd ~/opencv/build && \
    make -j $(nproc) && \
    make install && \
    ldconfig && \

    cp ~/opencv/build/lib/cv2.so /usr/local/lib/python2.7/dist-packages/

    # step 11
    # RUN cd ~/.virtualenvs/cv/lib/python2.7/site-packages/
    # RUN ln -s /usr/local/lib/python2.7/site-packages/cv2.so cv2.so

