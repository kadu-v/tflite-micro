FROM ubuntu:22.04

ENV DEBIAN_FRONTEND noninteractive
ENV LANG C.UTF-8
ENV TZ Asia/Tokyo
ENV NVIDIA_DRIVER_CAPABILITIES graphics

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN  apt update \
    && apt install -y sudo \
    && apt install -y xxd wget curl git xz-utils zip unzip --no-install-recommends 

# Clean Up
RUN	apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/* 

RUN	groupadd --gid $USER_GID $USERNAME \
    && useradd -s /bin/bash --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME \
    && su $USERNAME \
    && cd $HOME

RUN apt-get update && apt-get install -y \
    python3 \
    pip \
    make \
    ca-certificates \
    gcc-arm-none-eabi

RUN pip install --upgrade pip
RUN pip install numpy \
    yapf==0.32.0 \
    Pillow \
    Wave \
    pandas \
    matplotlib \
    six \
    pyyaml \
    requests \
    psutil \
    robotframework==4.0.1

RUN apt-get install -y lsb-release wget software-properties-common gnupg
RUN wget https://apt.llvm.org/llvm.sh
RUN chmod +x llvm.sh
RUN ./llvm.sh 16
RUN ln -s /usr/bin/clang-16 /usr/bin/clang
RUN ln -s /usr/bin/clang++-16 /usr/bin/clang++

RUN apt-get install clang-format-16
RUN ln -s /usr/bin/clang-format-16 /usr/bin/clang-format

# Needed when using the Dockerfile locally.
RUN git config --global --add safe.directory /opt/tflm



WORKDIR /workspaces
USER vscode