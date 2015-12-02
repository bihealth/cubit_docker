.PHONY: all build_system build_data run_data run_system

all:
	echo "Either use build or run"

build_system:
	sudo docker build -t cubit.ubuntu14.04 system

build_data:
	sudo docker build -t cubit.ubuntu14.04.data data

run_data:
	docker ps --all | grep cubit-ubuntu14.04-data >/dev/null \
		|| sudo docker run --name cubit-ubuntu14.04-data cubit.ubuntu14.04.data

run_system:
	sudo docker run \
		-t \
		-i \
		--volumes-from cubit-ubuntu14.04-data \
		-v /vol/local/data/cubit.env/cubit:/cubit \
		cubit.ubuntu14.04
