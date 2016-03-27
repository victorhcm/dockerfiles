[![Docker Pulls](https://img.shields.io/docker/pulls/victorhcm/opencv.svg)](https://hub.docker.com/r/victorhcm/opencv/)
[![Docker Stars](https://img.shields.io/docker/stars/victorhcm/opencv.svg)](https://hub.docker.com/r/victorhcm/opencv)

# opencv

OpenCV 3.1.0 + Python 2.7 bindings. Built following the [PyImageSearch guide][1].

## Usage

Create a new container:
```sh
$ docker run --name <CONTAINER_NAME> -it -v $(pwd):/host victorhcm/opencv /bin/bash
```

Detach using `Ctrl+p`+`Ctrl+q`.

Attach to a running docker container:

```sh
$ docker attach --sig-proxy=false <CONTAINER_NAME>
```

Start an existing docker container:
```sh
$ docker start <CONTAINER_NAME>
```

If you want a transient container, add `--rm` to remove the container after it stops (via @schickling):

```sh
$ docker run --rm -it -v $(pwd):/host victorhcm/opencv /bin/bash
```

### Compile

```sh
$ g++ $(pkg-config --cflags --libs opencv) my-file.cpp
```

## Issues

`$(pkg-config --cflags --libs opencv)` is returning a missing dependency `-lippicv`. The current workaround is to use the `pkg-config` output and manually remove `-lippicv`:

```sh
-I/usr/local/include/opencv -I/usr/local/include  -L/usr/local/lib -lopencv_stitching -lopencv_superres -lopencv_videostab -lopencv_aruco -lopencv_bgsegm -lopencv_bioinspired -lopencv_ccalib -lopencv_dnn -lopencv_dpm -lopencv_fuzzy -lopencv_line_descriptor -lopencv_optflow -lopencv_plot -lopencv_reg -lopencv_saliency -lopencv_stereo -lopencv_structured_light -lopencv_rgbd -lopencv_surface_matching -lopencv_tracking -lopencv_datasets -lopencv_text -lopencv_face -lopencv_xfeatures2d -lopencv_shape -lopencv_video -lopencv_ximgproc -lopencv_calib3d -lopencv_features2d -lopencv_flann -lopencv_xobjdetect -lopencv_objdetect -lopencv_ml -lopencv_xphoto -lopencv_highgui -lopencv_videoio -lopencv_imgcodecs -lopencv_photo -lopencv_imgproc -lopencv_core 
```

Another alternative is to use cmake. Here follows an example by [OpenCV][2]:

```cmake
# cmake needs this line
cmake_minimum_required(VERSION 2.8)

# Define project name
project(opencv_example_project)

# Find OpenCV, you may need to set OpenCV_DIR variable
# to the absolute path to the directory containing OpenCVConfig.cmake file
# via the command line or GUI
find_package(OpenCV REQUIRED)

# If the package has been found, several variables will
# be set, you can find the full list with descriptions
# in the OpenCVConfig.cmake file.
# Print some message showing some of them
message(STATUS "OpenCV library status:")
message(STATUS "    version: ${OpenCV_VERSION}")
message(STATUS "    libraries: ${OpenCV_LIBS}")
message(STATUS "    include path: ${OpenCV_INCLUDE_DIRS}")

if(CMAKE_VERSION VERSION_LESS "2.8.11")
  # Add OpenCV headers location to your include paths
  include_directories(${OpenCV_INCLUDE_DIRS})
endif()

# Declare the executable target built from your sources
add_executable(opencv_example example.cpp)

# Link your application with OpenCV libraries
target_link_libraries(opencv_example ${OpenCV_LIBS})
```

After adding the CMakeLists.txt file in the root of your project, create a build folder and compile:

```sh
mkdir project/build
cd project/build
cmake ..
make
```

[1]: www.pyimagesearch.com/2015/06/22/install-opencv-3-0-and-python-2-7-on-ubuntu/
[2]: https://github.com/Itseez/opencv/blob/master/samples/cpp/example_cmake/CMakeLists.txt
