# Makefile to build and run a Docker container

IMAGE_NAME := cpp_pubsub
DOCKERFILE := Dockerfile.runtime

build:
	docker build -t $(IMAGE_NAME) -f $(DOCKERFILE) .
	docker run -it --rm -v /var/run/docker.sock:/var/run/docker.sock -v /tmp:/tmp dslim/slim build --http-probe=false --continue-after=1 --cmd=talker --tag=$(IMAGE_NAME):talker cpp_pubsub
	docker run -it --rm -v /var/run/docker.sock:/var/run/docker.sock -v /tmp:/tmp dslim/slim build --http-probe=false --continue-after=1 --cmd=listener --tag=$(IMAGE_NAME):listener cpp_pubsub
	docker run -it --rm -v /var/run/docker.sock:/var/run/docker.sock -v /tmp:/tmp dslim/slim merge --tag=$(IMAGE_NAME):latest $(IMAGE_NAME):talker $(IMAGE_NAME):listener

clean:
	docker rmi $(IMAGE_NAME)