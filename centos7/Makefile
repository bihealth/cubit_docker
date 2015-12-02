.PHONY: all build_system build_data run_data run_system

all:
	echo "Either use build or run"

build_system:
	sudo docker build -t cubit.centos7 system

build_data:
	sudo docker build -t cubit.centos7.data data

run_data:
	docker ps --all | grep cubit-centos7-data >/dev/null \
		|| sudo docker run --name cubit-centos7-data cubit.centos7.data

run_system:
	sudo docker run \
		-t \
		-i \
		--volumes-from cubit-centos7-data \
		-v /vol/local/data/cubit.env/cubit:/cubit \
		cubit.centos7
