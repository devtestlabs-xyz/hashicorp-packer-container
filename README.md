# hashicorp-packer-container
## Overview
The purpose of this project is to manage an OCI-compliant [Hashicorp Packer](https://packer.io) container based on the official Alpine Linux image. This container image may be run in Docker and Podman.

## Getting Started
This project automatically builds containers for using the [`packer`](https://packer.io) command line program. The image is build and published to [Dockerhub devtestlabs/hashicorp-packer repo](https://hub.docker.com/r/devtestlabs/hashicorp-packer).

Releases are tagged from the `light` version. The `light` version just contains the current stable version of the Packer binary. The `latest` tag also points to this version.

You can use this version with the following:

*Docker*
```shell
docker run -i -t <args> devtestlabs/hashicorp-packer:light <command>
```

*Podman*
```shell
podman run -i -t <args> devtestlabs/hashicorp-packer:light <command>
```

*Podman example*
```shell
podman run -it devtestlabs/hashicorp-packer:light help
```

*NOTE: You may also simply pull the image from the Dockerhub repository. `podman pull devtestlabs/hashicorp-packer:light`.*

### Running a Packer build:

The easiest way to run a command that references a file is to bind mount the
file on the docker image:

*Docker*
```shell
docker run -it \
	--mount type=bind,source=/absolute/path/to/template.json,target=/mnt/template.json \
	devtestlabs/hashicorp-packer:latest build /mnt/template.json
```

*Podman*
```shell
podman run -it \
	--mount type=bind,source=/absolute/path/to/template.json:Z,target=/mnt/template.json \
	devtestlabs/hashicorp-packer:latest build /mnt/template.json
```

If you have several files you need Packer to have access to, you'll want to
bind mount a directory containing all of those files:

*Docker*
```shell
docker run -it \
    --mount type=bind,source=/absolute/path/to/test_docker_packer,target=/mnt/test_docker_packer \
    devtestlabs/hashicorp-packer:latest build \
    --var-file /mnt/test_docker_packer/vars.json \
    /mnt/test_docker_packer/template.json
```

*Podman*
```shell
podman run -it \
    --mount type=bind,source=/absolute/path/to/test_docker_packer:Z,target=/mnt/test_docker_packer \
    devtestlabs/hashicorp-packer:latest build \
    --var-file /mnt/test_docker_packer/vars.json \
    /mnt/test_docker_packer/template.json
```

## Dockerhub repository
https://hub.docker.com/r/devtestlabs/hashicorp-packer

## Build the image locally
You can build the container image locally:

*Docker*
```shell
cd dockerfiles/alpine

docker build -t my_local_packer .
```

*Podman*
```shell
cd dockerfiles/alpine

podman build -t my_local_packer .
```

## Learning more about Hashicorp Packer
Hashicorp has some of the best documentation in the business. Go read and get some hands on experience with Hashicorp Packer!

* [Hashicorp Learn Platform: Learning Packer](https://learn.hashicorp.com/packer)

* [Official Hashicorp Packer Guides](https://www.packer.io/guides)

* [Official Hashicorp Packer Docs](https://www.packer.io/docs)


## External References

* [Official Hashicorp Packer Container project](https://github.com/hashicorp/docker-hub-images/tree/master/packer)

* [Hashicorp Packer](https://packer.io)

* [Dockerhub: devtestlabs/hashicorp-packer repo](https://hub.docker.com/r/devtestlabs/hashicorp-packer)

* [Hashicorp Learn Platform: Learning Packer](https://learn.hashicorp.com/packer)

* [Official Hashicorp Packer Guides](https://www.packer.io/guides)

* [Official Hashicorp Packer Docs](https://www.packer.io/docs)