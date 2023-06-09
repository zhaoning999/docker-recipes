FROM nvidia/cuda:11.8.0-devel-ubuntu20.04
# Set TENSORRT_VERSION, example: 8.5.2-1+cuda11.8
ARG TENSORRT_VERSION=8.5.2-1+cuda11.8
# Set CUDNN_VERSION, example: 8.7.0.84-1+cuda11.8
ARG CUDNN_VERSION=8.7.0.84-1+cuda11.8

RUN sed -i 's@//.*archive.ubuntu.com@//mirrors.ustc.edu.cn@g' /etc/apt/sources.list

# Add open GL libraries
RUN apt-get update && \
        DEBIAN_FRONTEND=noninteractive  apt-get install -y --no-install-recommends \
        pkg-config \
        libglvnd-dev \
        libgl1-mesa-dev \
        libegl1-mesa-dev \
        libgles2-mesa-dev

RUN apt-get update && \
        DEBIAN_FRONTEND=noninteractive  apt-get install -y \
        wget \
        libyaml-cpp-dev \
        gnutls-bin

RUN apt-get update && \
        DEBIAN_FRONTEND=noninteractive  apt-get install -y \
        libgstreamer1.0-dev \
	libgstreamer-plugins-base1.0-dev \
	libgstreamer-plugins-bad1.0-dev \
	gstreamer1.0-plugins-base \
	gstreamer1.0-plugins-good \
	gstreamer1.0-plugins-bad \
	gstreamer1.0-plugins-ugly \
	gstreamer1.0-libav \
	gstreamer1.0-tools \
	gstreamer1.0-x \
	gstreamer1.0-alsa \
	gstreamer1.0-gl \
	gstreamer1.0-gtk3 \
	gstreamer1.0-qt5 \
	gstreamer1.0-pulseaudio

RUN apt-get update && \
        DEBIAN_FRONTEND=noninteractive         apt-get install -y --no-install-recommends \
        linux-libc-dev \
        libglew2.1 libssl1.1 libjpeg8 libjson-glib-1.0-0 \
        gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly gstreamer1.0-tools gstreamer1.0-libav \
        gstreamer1.0-alsa \
        libcurl4 \
        libuuid1 \
        libjansson4 \
        libjansson-dev \
        librabbitmq4 \
        libgles2-mesa \
        libgstrtspserver-1.0-0 \
        libv4l-dev \
        gdb bash-completion libboost-dev \
        uuid-dev libgstrtspserver-1.0-0 libgstrtspserver-1.0-0-dbg libgstrtspserver-1.0-dev \
        libgstreamer1.0-dev \
        libgstreamer-plugins-base1.0-dev \
        libglew-dev \
        libssl-dev \
        libopencv-dev \
        freeglut3-dev \
        libjpeg-dev \
        libcurl4-gnutls-dev \
        libjson-glib-dev \
        libboost-dev \
        librabbitmq-dev \
        libgles2-mesa-dev \
        pkg-config \
        libxau-dev \
        libxdmcp-dev \
        libxcb1-dev \
        libxext-dev \
        libx11-dev \
        libnss3 \
        linux-libc-dev \
        git \
        wget \
        gnutls-bin \
        sshfs \
        python3-distutils \
        python3-apt \
        python \
        rsyslog \
        vim  rsync \
        gstreamer1.0-rtsp \
        libcudnn8=${CUDNN_VERSION} \
        libcudnn8-dev=${CUDNN_VERSION} \
        libnvinfer8=${TENSORRT_VERSION} \
        libnvinfer-dev=${TENSORRT_VERSION} \
        libnvparsers8=${TENSORRT_VERSION} \
        libnvparsers-dev=${TENSORRT_VERSION} \
        libnvonnxparsers8=${TENSORRT_VERSION} \
        libnvonnxparsers-dev=${TENSORRT_VERSION} \
        libnvinfer-plugin8=${TENSORRT_VERSION} \
        libnvinfer-plugin-dev=${TENSORRT_VERSION} \
        python3-libnvinfer=${TENSORRT_VERSION} \
        python3-libnvinfer-dev=${TENSORRT_VERSION} && \
        rm -rf /var/lib/apt/lists/* && \
        apt autoremove

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
    libx11-xcb-dev \
    libxkbcommon-dev \
    libwayland-dev \
    libxrandr-dev \
    libegl1-mesa-dev && \
    rm -rf /var/lib/apt/lists/*

# Install DeepStreamSDK using Debian package. DeepStream tar package can also be installed in a similar manner
ADD deepstream-6.2_6.2.0-1_amd64.deb /root

RUN apt-get update && \
      DEBIAN_FRONTEND=noninteractive  apt-get install -y --no-install-recommends \
      /root/deepstream-6.2_6.2.0-1_amd64.deb && \
      rm -rf /root/deepstream-6.2_6.2.0-1_amd64.deb

WORKDIR /opt/nvidia/deepstream/deepstream

RUN ln -s /usr/lib/x86_64-linux-gnu/libnvcuvid.so.1 /usr/lib/x86_64-linux-gnu/libnvcuvid.so
RUN ln -s /usr/lib/x86_64-linux-gnu/libnvidia-encode.so.1 /usr/lib/x86_64-linux-gnu/libnvidia-encode.so

# To get video driver libraries at runtime (libnvidia-encode.so/libnvcuvid.so)
ENV NVIDIA_DRIVER_CAPABILITIES $NVIDIA_DRIVER_CAPABILITIES,video,compute,graphics,utility

