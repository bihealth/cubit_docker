.PHONY: all build_system build_data run_data run_system

all:
	echo "Either use build or run"

build_system:
	sudo docker build -t cubit.debian8 system

build_data:
	sudo docker build -t cubit.debian8.data data

run_data:
	docker ps --all | grep cubit-debian8-data >/dev/null \
		|| sudo docker run --name cubit-debian8-data cubit.debian8.data

run_system:
	sudo docker run \
		-t \
		-i \
		--volumes-from cubit-debian8-data \
		-v /vol/local/data/cubit.env/cubit:/cubit \
		cubit.debian8
