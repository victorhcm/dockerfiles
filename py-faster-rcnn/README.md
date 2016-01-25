# py-faster-rcnn


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

