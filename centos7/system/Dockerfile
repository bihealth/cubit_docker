FROM centos:7

ENV http_proxy=http://proxy.charite.de:8080
ENV https_proxy=http://proxy.charite.de:8080

# Add group and user first so they are assigned consistently
RUN groupadd cubit -g 5000 \
    && useradd -u 5005 -g cubit cubit

# Install required packages
RUN yum install -y \
    autoconf \
    automake \
    bzip2 \
    bzip2-devel \
    environment-modules \
    gawk \
    gcc \
    gcc-c++ \
    git \
    libbz2-devel \
    libdb-devel \
    libibverbs-devel \
    libpng12 \
    libXt-devel \
    libxml2-devel \
    lzo-devel \
    m4 \
    make \
    mlocate \
    ncurses-libs \
    openssl-devel \
    patch \
    perl \
    perl-Data-Dumper \
    perl-List-MoreUtils \
    pth \
    python-devel \
    sqlite-devel \
    tar \
    unzip \
    vim-common \
    wget \
    zip

# Update cubit's .bashrc
RUN echo "module use /cubit/tools/easybuild/modules/all" >> /home/cubit/.bashrc && \
        echo "module load EasyBuild" >> /home/cubit/.bashrc

# Switch to cubit user
USER cubit

# Go to /home/cubit after login
WORKDIR /home/cubit

# Fetch easybuild script
RUN curl -o /home/cubit/bootstrap_eb.py \
        https://raw.githubusercontent.com/hpcugent/easybuild-framework/develop/easybuild/scripts/bootstrap_eb.py
