# Description

This is the official Inception framework docker build script.

# Installation

## Prerequisite

Refer to the docker official website for installation instructions (Docker Community Edition).
https://docs.docker.com/install/linux/docker-ce/ubuntu/

## Building the docker image

Use the command bellow to start the installation.

```
$ docker build --no-cache host -t inception/inception .
```

## Troubles

### Network isolation bypass

The '--network' option enables docker container to bypass network isolation and get a direct access to the host network interface.

### Disable cache

If builds fail for some reason but fresh update of the code is not needed remove 
--no-cache this allows docker to reuse what was compiled before.

### Limit resources use

If docker uses too much resources you can throttle CPU resources or memory by adding (limit to 8GB ram and swap and 2 CPU Cores):
--memory="8g" --memory-swap="8g" --cpu-period=100000 --cpu-quota=200000 


Beware that the default compilation uses 12 parallel jobs (-j12) which may use
too much memory and lead to compilation failure (oom killed), in that case it is
possible to limit the CPUs used with the MAKE_JOBS parameter by setting it to a given value or  . 

```
$ docker build --memory="8g" --memory-swap="8g" --cpu-period=100000 --cpu-quota=200000 --build-arg  MAKE_JOBS=2 --no-cache --network host -t inception/inception .
```

it is also possible to use just the right number of jobs with:
```
MAKE_JOBS=$(($(nproc 2> /dev/null || echo ${MAKE_JOBS})+1)) 
```

# Use
```
docker run -i -t inception/inception /bin/bash
```
