# Choose the base distro based on the supported ones for the used yocto version. E.g. ubuntu-24.04 for scarthgap.
ARG BASE_DISTRO

FROM crops/yocto:${BASE_DISTRO}-base

USER root

RUN apt-get update && apt-get install -y --no-install-recommends \
    wget \
    parted \
    mtools \
    minicom \
    dfu-util \
    usbutils \
    && rm -rf /var/lib/apt/lists/*

RUN wget -O /usr/local/bin/uuu \
    https://github.com/nxp-imx/mfgtools/releases/download/uuu_1.5.243/uuu \
 && chmod +x /usr/local/bin/uuu

RUN pip3 install --break-system-packages oelint-adv
RUN pip3 install --break-system-packages bitbake-setup

RUN userdel -r ubuntu; usermod -u 1000 yoctouser; groupmod -g 1000 yoctouser
RUN chsh -s /bin/bash yoctouser

RUN mkdir /yocto-shared
RUN chown -R 1000:1000 /yocto-shared

USER yoctouser