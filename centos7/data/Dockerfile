FROM centos:7

ENV http_proxy=http://proxy.charite.de:8080
ENV https_proxy=http://proxy.charite.de:8080

# Add group and user first so they are assigned consistently
RUN groupadd cubit -g 5000 \
    && useradd -u 5005 -g cubit cubit

RUN mkdir -p \
        /cubit/tools/easybuild.local \
        /cubit/tools/easybuild/build \
        /cubit/tools/easybuild/ebfiles_repo \
        /cubit/tools/easybuild/modules \
        /cubit/tools/easybuild/software

RUN chown cubit:cubit -R /cubit \
        && chmod ug=rwX,a=rX /cubit

VOLUME /cubit/tools/easybuild.local
VOLUME /cubit/tools/easybuild/build
VOLUME /cubit/tools/easybuild/ebfiles_repo
VOLUME /cubit/tools/easybuild/modules
VOLUME /cubit/tools/easybuild/software
