# # https://hub.docker.com/_/ubuntu/
# ARG UBUNTU_VERSION=20.04
# ARG OPENCV_VERSION=4.5.4

# FROM ubuntu:$UBUNTU_VERSION

# RUN apt-get update && apt-get install -y --no-install-recommends

# # ENV TZ=Europe/London
# # RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# # ---------------------------
# # | INSTALL ADDITIONAL APTs |
# # ---------------------------
# RUN apt-get update && apt-get install -y --no-install-recommends \
#     build-essential \
#     git \
#     curl \
#     ca-certificates \
#     ssh \
#     nano \
#     htop \
#     unzip \
#     wget \
#     apt-transport-https \
#     ca-certificates


# ###################
# RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
#     pkg-config \
#     cmake

# RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
#     libx11-dev \
#     libxft-dev \
#     autoconf \
#     libtool \
#     bison \
#     gperf \
#     libgles2-mesa-dev \
#     libxext-dev \
#     libxrandr-dev \
#     libxi-dev \
#     libxcursor-dev \
#     libxdamage-dev \
#     libxinerama-dev

# RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
#     curl \
#     git \
#     tar \
#     zip \
#     unzip

# RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
#     python3 \
#     python3-pip 

# RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
#     autoconf \
#     automake \
#     libtool

# ## 
# RUN git clone https://github.com/Microsoft/vcpkg.git /opt/vcpkg
# WORKDIR /opt/vcpkg

# RUN ./bootstrap-vcpkg.sh \
#     && ./vcpkg integrate install \
#     && ./vcpkg integrate bash \
#     && echo 'export PATH=$PATH:/opt/vcpkg' >>~/.bashrc

# # WORKDIR /root

# # ARG build_parent_dir='/usr/local/c++'

# # # git checkout 54f55a526804f99a1eb4c798ccd085e8dab74492 -- opencv 4.5.4 port
# # RUN echo $build_parent_dir && \
# #     mkdir -p ${build_parent_dir} && \
# #     chmod -R 777 ${build_parent_dir} && \
# #     cd ${build_parent_dir} && \
# #     git clone https://github.com/Microsoft/vcpkg.git && \
# #     cd vcpkg && git checkout 54f55a526804f99a1eb4c798ccd085e8dab74492 && \
# #     ./bootstrap-vcpkg.sh && \
# #     ./vcpkg integrate install && \
# #     ./vcpkg install crow && \
# #     ./vcpkg install numcpp && \
# #     ./vcpkg install opencv4[dnn]


# RUN ls

# # # | SETUP WORKSPACE |
# # # -------------------
# # WORKDIR /workspace

# # COPY run.sh /
# # RUN chmod +x /run.sh
# # CMD "/run.sh"

# CMD ["bash"]

FROM ubuntu:18.04
# Update the system so that the public apt repositry locations are visible
RUN apt update -y && apt upgrade -y

# -------------------------------------------------
# | Install g++ 7.5 and other necessary libraries |
# -------------------------------------------------
RUN apt install -y build-essential cmake git 

#     libgtk-3-dev \
#     libavcodec-dev libavformat-dev libswscale-dev \
#     libgstreamer-plugins-base1.0-dev libgstreamer1.0-dev


# ---------------------------
# | Install open cv version 4.5.5|
# ---------------------------

## If static linking then remove libpng system package otherwise opencv will not install it use systems shared library and it will cause issue in cmake
## build for library 'opencv_imgcodecs' --- more info -- libpng installed by apt install libgtk-3-dev
RUN apt remove libpng-dev

RUN cd && mkdir opencv_build && cd opencv_build && git clone --progress --verbose https://github.com/opencv/opencv.git && git clone --progress --verbose https://github.com/opencv/opencv_contrib.git && cd ~/opencv_build/opencv && git checkout --progress tags/4.5.5 && \
    cd ~/opencv_build/opencv_contrib && git checkout --progress tags/4.5.5 && \
    mkdir ~/opencv_build/opencv/build && cd ~/opencv_build/opencv/build
	
# BUILD_SHARED_LIBS=OFF -- for building static files
# WITH_OPENCL=OFF -- turn off unused package from build
# And turn off all Video I/O utils -- from -WITH_V4L to -DWITH_1394
RUN cd ~/opencv_build/opencv/build && \
    cmake -D CMAKE_INSTALL_PREFIX=/usr/local \
    -D BUILD_SHARED_LIBS=OFF \
    -D BUILD_ZLIB=ON \
    -D WITH_OPENCL=OFF \
    -D WITH_V4L=OFF -DWITH_FFMPEG=OFF -DWITH_GSTREAMER=OFF \
    -D WITH_MSMF=OFF -DWITH_DSHOW=OFF -DWITH_AVFOUNDATION=OFF -DWITH_1394=OFF \
    -D OPENCV_EXTRA_MODULES_PATH=~/opencv_build/opencv_contrib/modules ..

RUN cd ~/opencv_build/opencv/build && \
    make -j5 && make install 

# RUN rm -rf ~/opencv_build

RUN ls


