FROM ubuntu:18.04

RUN apt-get update && apt-get install -y \
    autoconf \
    automake \
    autopoint \
    build-essential \
    git \
    gettext \
    libaa1-dev \
    libcdk5-dev \
    libexif-dev \
    libjpeg-dev \
    libpopt-dev \
    libreadline-dev \
    libtool \
    libusb-dev \
    pkg-config \
    wget \
 && rm -rf /var/lib/apt/lists/*

RUN mkdir /workspace
WORKDIR /workspace

# Download linuxdeploy appimage for packaging
# Verify SHA512 checksum. The silly thing is linuxdeploy only provides a continuous build, no tagged release builds. So this will likely need to be manually updated.
RUN wget --directory-prefix=/workspace https://github.com/linuxdeploy/linuxdeploy/releases/download/continuous/linuxdeploy-x86_64.AppImage && \
    [ "15b26c6b185709a15a604b3f59df30cfc4676108abc53135b5192496be11d30dc8ee680ee1382f116eb58f47e0dbb4094df7c72bccb683b9fded0f74aa7e1ffa  /workspace/linuxdeploy-x86_64.AppImage" = "$(sha512sum /workspace/linuxdeploy-x86_64.AppImage)" ]

RUN chmod +x /workspace/linuxdeploy-x86_64.AppImage

# Copy scripts
COPY build-appimage /workspace/build-appimage

VOLUME /workspace/gphoto2
VOLUME /workspace/libgphoto2

CMD ["/workspace/build-appimage"]

