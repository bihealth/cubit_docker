.PHONY: all build_system build_data run_data run_system

all:
	echo "Either use build or run"

%/Dockerfile: %/Dockerfile.in
	cp $< $@
	perl -p -i -e "s/__GID__/$$(id -g)/g" $@
	perl -p -i -e "s/__UID__/$$(id -u)/g" $@
	if [ -n "$$http_proxy" ]; then \
		perl -p -i -e "s|ENV http_proxy=|ENV http_proxy=$$http_proxy|g" $@; \
		perl -p -i -e "s|ENV https_proxy=|ENV https_proxy=$$https_proxy|g" $@; \
	else \
		perl -p -i -e "s|ENV http_proxy=|#ENV http_proxy=|g" $@; \
		perl -p -i -e "s|ENV https_proxy=|#ENV https_proxy=|g" $@; \
	fi

build_system: system/Dockerfile
	docker build -t cubit.debian8 system

build_data: data/Dockerfile
	docker build -t cubit.debian8.data data

run_data:
	docker ps --all | grep cubit-debian8-data >/dev/null \
		|| docker run --name cubit-debian8-data cubit.debian8.data

run_system:
	docker run \
		-t \
		-i \
		--volumes-from cubit-debian8-data \
		-v /vol/local/data/cubit.env/cubit:/cubit \
		cubit.debian8
