# Cubit in Docker

This project contains Makefiles and Dockerfiles for a completely containerized environment of Cubit.
This allows for easy, isolated installation and building of Cubit.

## Prerequisites

- Only tested on Ubuntu 14.04 as the host system
- Install Docker following the instructions of the nice people over at Docker
- Install git
- Yay, you're done

## Installation

- Checkout `cubit_docker`

```
# git clone https://github.com/bihealth/cubit_docker.git
```

- Inside, create a new checkout of cubit (will be ignored by the cubit_docker Git repository)

```
# cd cubit_docker
# git clone https://github.com/bihealth/cubit.git
```

- Follow the [Provide required non-distributable software](https://github.com/bihealth/cubit/blob/master/tools/README.md#provide-required-non-distributable-software) step from the Cubit installation.

## Build System Image

The description here is for `centos7` but it should work for `ubuntu14.04` and `debian8` as well.

Make sure that the environment variables `http_proxy` and `https_proxy` are set if necessary.
They will also be set within the `Dockerfile`.

Adjust `centos7/Makefile` and change `/vol/local/data/data/cubit.env/cubit` to the path to your cubit checkout.

Then, execute the following:

```
# cd centos7
# make build
```

The next step is to start the Docker container and perform the Cubit installation.
Note that the `cubit` Git checkout is meant to be **shared** by all containers.
This has the advantage that updates are visible immediately by all containers.
On the other hand, any git command performing an update must only be run by one container.
After the updating step (in particular the one involving Git LFS) is complete, you can run the compilation in multiple containers concurrently.

```
# make run prefix=<INSTALLPATH>
(inside the container)
# ./buildscript.sh <INSTALLPATH>
```
You are done!
