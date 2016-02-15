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

[1]: www.pyimagesearch.com/2015/06/22/install-opencv-3-0-and-python-2-7-on-ubuntu/
