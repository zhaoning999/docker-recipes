build Docker file

```bash

# download deepstream-6.2_6.2.0-1_amd64.deb
docker build -t deepstream-6.2-11.8 .

# build opencv

sudo apt-get install build-essential cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev libdc1394-22-dev

wget https://github.com/opencv/opencv/archive/refs/tags/4.7.0.tar.gz -O opencv-4.7.0.tar.gz

tar xvf opencv-4.7.0.tar.gz && cd opencv-4.7.0 && mkdir build && cd build

cmake -D CMAKE_BUILD_TYPE=Release -D BUILD_EXAMPLES=OFF \
	-D BUILD_DOCS=OFF -D BUILD_PERF_TESTS=OFF \
    -D BUILD_opencv_python2=OFF \
    -D BUILD_TESTS=OFF -D CMAKE_INSTALL_PREFIX=/root/learn/opencv-4.7.0 ..

make -j$(nproc) && make install


# build protobuf

 wget https://ghps.cc/https://github.com/protocolbuffers/protobuf/archive/refs/tags/v3.19.6.tar.gz -O protobufv3.19.6.tar.gz

tar xvf protobuf-3.19.6.tar.gz && cd protobuf-3.19.6 && mkdir build && cd build

cmake -DCMAKE_CXX_STANDARD=14 -D CMAKE_INSTALL_PREFIX=/root/learn/protobuf-3.19.6 \
    -Dprotobuf_BUILD_TESTS=OFF ../cmake

make -j$(nproc) && make install

```
