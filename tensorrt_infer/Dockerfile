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
	libnvinfer-samples=${TENSORRT_VERSION} \
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
RUN apt-get update && \
      DEBIAN_FRONTEND=noninteractive  apt-get install -y --no-install-recommends \
      build-essential \
      cmake \
      git \
      libgtk2.0-dev \
      pkg-config \
      libavcodec-dev \
      libavformat-dev \
      libswscale-dev \
      libtbb2 \
      libtbb-dev \
      libjpeg-dev \
      libpng-dev \
      libtiff-dev \
      libdc1394-22-dev \
      wget \
      unzip

# fastgithub

ARG FASTGITHUB_URL=https://ghps.cc/https://github.com/dotnetcore/FastGithub/releases/download/2.1.4/fastgithub_linux-x64.zip

RUN wget ${FASTGITHUB_URL} -O /root/fastgithub_linux-x64.zip && \
    cd /root && \
    unzip fastgithub_linux-x64.zip && \
    rm -rf /root/fastgithub_linux-x64.zip

# RUN nohup /root/fastgithub_linux-x64/fastgithub > /dev/null 2>&1 &

# opencv
ARG OPENCV_VERSION=4.7.0
ARG OPENCV_URL=https://ghps.cc/https://github.com/opencv/opencv/archive/refs/tags/${OPENCV_VERSION}.tar.gz
ARG OPENDV_DIR=/root/opencv-${OPENCV_VERSION}
ARG OPENDV_INSTALL_DIR=/root/learn/opencv-${OPENCV_VERSION}

ADD opencv-4.7.0/.cache /root/opencv-4.7.0
RUN wget ${OPENCV_URL} -O ${OPENDV_DIR}.tar.gz && \
    tar xvf ${OPENDV_DIR}.tar.gz -C /root && \
    mkdir -p ${OPENDV_DIR}/build && \
    cd ${OPENDV_DIR}/build && \
    cmake -DCMAKE_BUILD_TYPE=Release \
        -DBUILD_EXAMPLES=OFF \
        -DBUILD_DOCS=OFF \
        -DBUILD_PERF_TESTS=OFF \
        -DBUILD_opencv_python2=OFF \
        -DBUILD_TESTS=OFF \
        -DCMAKE_INSTALL_PREFIX=${OPENDV_INSTALL_DIR} \
        .. && \
    make -j$(nproc) && make install && \
    rm -rf ${OPENDV_DIR} && \
    rm -rf ${OPENDV_DIR}.tar.gz

ARG PROTOBUF_VERSION=3.19.6
ARG PROTOBUF_URL=https://ghps.cc/https://github.com/protocolbuffers/protobuf/archive/refs/tags/v${PROTOBUF_VERSION}.tar.gz
ARG PROTOBUF_DIR=/root/protobuf-${PROTOBUF_VERSION}
ARG PROTOBUF_INSTALL_DIR=/root/learn/protobuf-${PROTOBUF_VERSION}

RUN wget ${PROTOBUF_URL} -O ${PROTOBUF_DIR}.tar.gz && \
    tar xvf ${PROTOBUF_DIR}.tar.gz -C /root && \
    mkdir -p ${PROTOBUF_DIR}/build && \
    cd ${PROTOBUF_DIR}/build && \
    cmake -DCMAKE_CXX_STANDARD=14 \
        -DCMAKE_INSTALL_PREFIX=${PROTOBUF_INSTALL_DIR} \
        -Dprotobuf_BUILD_TESTS=OFF \
        ../cmake && \
    make -j$(nproc) && make install && \
    rm -rf ${PROTOBUF_DIR} && \
    rm -rf ${PROTOBUF_DIR}.tar.gz 

# To get video driver libraries at runtime (libnvidia-encode.so/libnvcuvid.so)
ENV NVIDIA_DRIVER_CAPABILITIES $NVIDIA_DRIVER_CAPABILITIES,video,compute,graphics,utility

# cmake -DCMAKE_BUILD_TYPE=Release \
#     -DBUILD_EXAMPLES=OFF \
#     -DBUILD_DOCS=OFF \
#     -DBUILD_PERF_TESTS=OFF \
#     -DBUILD_opencv_python2=OFF \
#     -DBUILD_TESTS=OFF \
#     -DCMAKE_INSTALL_PREFIX=/root/learn/opencv-4.7.0 \
#     ..
