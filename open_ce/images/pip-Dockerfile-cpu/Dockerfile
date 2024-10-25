FROM registry.access.redhat.com/ubi9/ubi

ENV CICD_GROUP=cicd
ARG GROUP_ID=1500
ENV BUILD_USER=builder
ARG BUILD_ID=1084

RUN export ARCH="$(uname -m)" && \
    yum install -y git make gcc-toolset-13 python3.12-pip python3.12 python3.12-devel unzip java-11-openjdk java-11-openjdk-devel zip cmake wget && \
    # Create CICD Group
    groupadd --non-unique --gid ${GROUP_ID} ${CICD_GROUP} && \
    # Adduser Builder
    useradd -b /home --non-unique --create-home --gid ${GROUP_ID} --groups wheel \
    --uid ${BUILD_ID} --comment "User for Building" ${BUILD_USER} && \
    pip3.12 install virtualenv && \
    ln -s /usr/bin/python3.12 /usr/local/bin/python

USER ${BUILD_USER}
RUN export PATH="/opt/rh/gcc-toolset-13/root/usr/bin:${PATH}" && \
    export GCC_HOME="/opt/rh/gcc-toolset-13/root/usr" && \
    echo "PATH="${PATH}"" >> ${HOME}/.profile && \
    echo "PATH="${PATH}"" >> ${HOME}/.bashrc && \
    echo "GCC_HOME="${GCC_HOME}"" >> ${HOME}/.bashrc
