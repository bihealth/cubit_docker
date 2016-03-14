.PHONY: build run

PREFIX=/scratch/cubit

default: run

build:
	docker build \
		--build-arg PREFIX=$(PREFIX) \
		-t \
		cubit.centos7 \
		.

run: build
	docker run -it \
		--env HOME=/tmp \
		-u $(shell id -u):$(shell id -g) \
		-v /vol/local/data/cubit.env/cubit:/cubit.env \
		-v /vol/local/data/cubit.env/centos7:$(PREFIX) \
		--workdir /cubit.env/tools \
		cubit.centos7 \
		bash --login ./buildscript.sh \
			-a haswell \
			$(PREFIX)
	docker run -it \
		--env HOME=/tmp \
		-u $(shell id -u):$(shell id -g) \
		-v /vol/local/data/cubit.env/cubit:/cubit.env \
		-v /vol/local/data/cubit.env/centos7:$(PREFIX) \
		--workdir /cubit.env/tools \
		cubit.centos7 \
		bash --login ./buildscript.sh \
			-a haswell \
			-e \
			$(PREFIX)
