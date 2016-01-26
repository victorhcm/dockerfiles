FROM kaixhin/cuda-caffe
MAINTAINER Victor Melo <victorhcmelo@gmail.com>

# Install dependencies
RUN \ 
    apt-get update && apt-get upgrade -y && \

    apt-get install python-opencv -y && \
    apt-get install python-pip -y && \

    pip install --upgrade pip && \
    pip install cython && \
    pip install easydict

# clean stuff
#     apt-get autoclean && apt-get clean && \
# 
#     rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


# Install py-faster-rcnn
RUN \
    cd /root && \
    git clone --recursive https://github.com/rbgirshick/py-faster-rcnn.git && \
    cd /root/py-faster-rcnn/lib && \
    make && \

    cd /root/py-faster-rcnn/caffe-fast-rcnn && \
    make -j $(nproc) && \
    make pycaffe
