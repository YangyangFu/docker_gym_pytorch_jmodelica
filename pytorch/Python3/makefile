#DOCKER_ORG = yangyangfu
DOCKER_ORG = $(shell docker info 2>/dev/null | sed '/Username:/!d;s/.* //')
IMA_NAME = pytorch
DOCKER_FULL_NAME = $(DOCKER_ORG)/$(IMA_NAME)

ifeq ("$(DOCKER_ORG)","")
$(warning WARNING: No docker user found using results from whoami)
DOCKER_ORG       = $(shell whoami)
endif

PYTORCH_VERSION = 1.5.0
CUDA_VERSION = 10.2
BASE_RUNTIME = ubuntu:18.04

PYTHON_VERSION = 3.8

#DOCKER_TAG = $(CUDA_VERSION)-cudnn$(CUDNN_VERSION)-$(BASE_RUNTIME)
DOCKER_TAG = $(PYTORCH_VERSION)-cuda$(CUDA_VERSION)

COMMAND_RUN = docker run \
	  --name c1 \
	  --detach=false \
	  -e DISPLAY=${DISPLAY} \
	  -v /tmp/.X11-unix:/tmp/.X11-unix \
	  --rm \
	  -v `pwd`:/mnt/shared \
	  -i \
      -t \
	  ${DOCKER_FULL_NAME}:${DOCKER_TAG} /bin/bash -c

build:
	docker build --no-cache --rm -t ${DOCKER_FULL_NAME}:${DOCKER_TAG} .

remove_image:
	docker rmi ${DOCKER_FULL_NAME}:${DOCKER_TAG}

push:
	docker push ${DOCKER_FULL_NAME}:${DOCKER_TAG}

Run:
	${COMMAND_RUN} \
		"cd /mnt/shared && bash"