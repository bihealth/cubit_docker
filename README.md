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

## Build Data and System Image

The description here is for `centos7` but it should work for `ubuntu14.04` and `debian8` as well.

First, edit `centos7/data/Dockerfile` and `centos7/system/Dockerfile` and replace the UID 5005 and GID 5000 by your local UID and GID.
Also, update the lines defining `http_proxy` and `https_proxy` to reflect the proxy settings in your organization or remove these lines if you do not need a proxy for HTTP(S).

Adjust `centos7/Makefile` and change `/vol/local/data/cubit.env/cubit` to the path to your cubit checkout.

Then, execute the following:

```
# cd centos7
# make build_data
# make run_data
# make build_system
```

The `make run_data` will create a data image that will host our data.
In our Docker container that we use for the installation, we will mount the volumes from the created image (`cubit-centos7-data`).
Further, we map the `cubit` directory that we cloned via Git into the container.

The next step is to start the Docker container and perform the Cubit installation.
Note that the `cubit` Git checkout is meant to be **shared** by all containers.
This has the advantage that updates are visible immediately by all containers.
On the other hand, any git command performing an update must only be run by one container.
After the updating step (in particular the one involving Git LFS) is complete, you can run the compilation in multiple containers concurrently.

```
# make run_system
(inside the container)
# cd /cubit/tools
# ./buildscript.sh /cubit/tools
```
