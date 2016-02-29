.PHONY: all build_system build_data run_data run_system

all:
	echo "Either use build or run"

%/Dockerfile: %/Dockerfile.in
	cp $< $@
	perl -p -i -e "s/__GID__/$$(id -g)/g" $@
	perl -p -i -e "s/__UID__/$$(id -u)/g" $@
	perl -p -i -e "s/__prefix__/$$prefix/g" $@
	if [ -n "$$http_proxy" ]; then \
		perl -p -i -e "s|ENV http_proxy=|ENV http_proxy=$$http_proxy|g" $@; \
		perl -p -i -e "s|ENV https_proxy=|ENV https_proxy=$$https_proxy|g" $@; \
	else \
		perl -p -i -e "s|ENV http_proxy=|#ENV http_proxy=|g" $@; \
		perl -p -i -e "s|ENV https_proxy=|#ENV https_proxy=|g" $@; \
	fi

build_system: system/Dockerfile
	docker build -t cubit.centos7 system

build_data: data/Dockerfile
	docker build -t cubit.centos7.data data

run_data:
	docker ps --all | grep cubit-centos7-data >/dev/null \
		|| docker run --name cubit-centos7-data cubit.centos7.data

run_system:
	docker run \
        -it \
		-v /vol/local/data/data/cubit.env/cubit:/cubit.env \
 		-v /vol/local/data/data/cubit.env/centos7:$(prefix) \
		cubit.centos7
