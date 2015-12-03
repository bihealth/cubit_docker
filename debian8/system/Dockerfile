FROM debian:8

ENV http_proxy=http://proxy.charite.de:8080
ENV https_proxy=http://proxy.charite.de:8080

# Add group and user first so they are assigned consistently
RUN groupadd --gid 5000 cubit \
    && adduser --uid 5005 --gid 5000 cubit

# Install required packages
RUN apt-get update
RUN apt-get install -y \
     cpio \
     curl \
     environment-modules \
     git \
     less \
     libbz2-dev \
     libc6-dev-i386 \
     libdb-dev \
     libfreetype6-dev \
     libibverbs-dev \
     liblist-moreutils-perl \
     liblzo2-dev \
     libssl-dev \
     libtinfo-dev \
     libx11-dev \
     libxml2-dev \
     pkg-config \
     python \
     python2.7 \
     unzip \
     vim-nox \
     wget \
     xorg-dev \
     zip

# Update cubit's .bashrc
RUN echo "typeset -f module > /dev/null" >> /home/cubit/.bashrc && \
        echo "if [ \$? != 0 -a -r /etc/profile.d/modules.sh ]; then" >> /home/cubit/.bashrc && \
        echo "    source /etc/profile.d/modules.sh" >> /home/cubit/.bashrc && \
        echo "fi" >> /home/cubit/.bashrc

RUN echo "module use /cubit/tools/easybuild/modules/all" >> /home/cubit/.bashrc && \
        echo "module load EasyBuild" >> /home/cubit/.bashrc && \
        echo "export PYTHONPATH=\$PYTHONPATH:/cubit/tools/easybuild.local" >> /home/cubit/.bashrc

# Switch to cubit user
USER cubit

# Go to /home/cubit after login
WORKDIR /home/cubit

# Fetch easybuild script
RUN curl -o /home/cubit/bootstrap_eb.py https://raw.githubusercontent.com/hpcugent/easybuild-framework/develop/easybuild/scripts/bootstrap_eb.py
