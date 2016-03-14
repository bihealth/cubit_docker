# CentOS image for cubit
#
# Build with
#
#       docker build [--build-arg PREFIX=/cubit] -t cubit.centos7 .
#
# Run with
#
#       docker run -it \
#           -u ${UID}:${GROUPS} \
#           -v /vol/local/data/data/cubit.env/cubit:/cubit.env \
#           -v /vol/local/data/data/cubit.env/centos7:/cubit \
#           cubit.centos7
FROM centos:7

# Install prefix, can be changed with docker build --build-arg PREFIX=/other
ARG PREFIX=/cubit

# Install EPEL, for more packages
RUN rpm -iUvh http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-5.noarch.rpm

# Install required packages
RUN yum update -y && \
    yum install -y \
        autoconf \
        automake \
        bzip2 \
        bzip2-devel \
        environment-modules \
        file \
        gawk \
        gcc \
        gcc-c++ \
        git \
        libbz2-devel \
        libdb-devel \
        libibverbs-devel \
        libpng12 \
        libpng-devel \
        libXt-devel \
        libxml2-devel \
        lzo-devel \
        m4 \
        make \
        mariadb-devel \
        mlocate \
        ncurses-libs \
        openssl-devel \
        patch \
        perl \
        perl-Data-Dumper \
        perl-List-MoreUtils \
        pth \
        python-devel \
        python-pip \
        sqlite-devel \
        tar \
        tcsh \
        unzip \
        vim-common \
        wget \
        which \
        zip

# Append module loading to system-wide profile file
RUN echo "typeset -f module > /dev/null" >> /etc/profile && \
        echo "source /etc/profile.d/modules.sh" >> /etc/profile && \
        echo "module use $PREFIX/current/tools/easybuild/modules/all" >> /etc/profile && \
        echo "module load EasyBuild" >> /etc/profile && \
        echo "export PYTHONPATH=\$PYTHONPATH:$PREFIX/current/tools/easybuild.local" >> /etc/profile
RUN source /etc/profile

# Install modern version of setuptools via pip
RUN pip install setuptools==19.4
