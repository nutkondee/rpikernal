Linux kernel
============

There are several guides for kernel developers and users. These guides can
be rendered in a number of formats, like HTML and PDF. Please read
Documentation/admin-guide/README.rst first.

In order to build the documentation, use ``make htmldocs`` or
``make pdfdocs``.  The formatted documentation can also be read online at:

    https://www.kernel.org/doc/html/latest/

There are various text files in the Documentation/ subdirectory,
several of them using the Restructured Text markup notation.

Please read the Documentation/process/changes.rst file, as it contains the
requirements for building and running the kernel, and information about
the problems which may result by upgrading your kernel.

Build status for rpi-5.15.y:
[![Pi kernel build tests](https://github.com/raspberrypi/linux/actions/workflows/kernel-build.yml/badge.svg?branch=rpi-5.15.y)](https://github.com/raspberrypi/linux/actions/workflows/kernel-build.yml)
[![dtoverlaycheck](https://github.com/raspberrypi/linux/actions/workflows/dtoverlaycheck.yml/badge.svg?branch=rpi-5.15.y)](https://github.com/raspberrypi/linux/actions/workflows/dtoverlaycheck.yml)

Build status for rpi-6.1.y:
[![Pi kernel build tests](https://github.com/raspberrypi/linux/actions/workflows/kernel-build.yml/badge.svg?branch=rpi-6.1.y)](https://github.com/raspberrypi/linux/actions/workflows/kernel-build.yml)
[![dtoverlaycheck](https://github.com/raspberrypi/linux/actions/workflows/dtoverlaycheck.yml/badge.svg?branch=rpi-6.1.y)](https://github.com/raspberrypi/linux/actions/workflows/dtoverlaycheck.yml)

Build status for rpi-6.6.y:
[![Pi kernel build tests](https://github.com/raspberrypi/linux/actions/workflows/kernel-build.yml/badge.svg?branch=rpi-6.6.y)](https://github.com/raspberrypi/linux/actions/workflows/kernel-build.yml)
[![dtoverlaycheck](https://github.com/raspberrypi/linux/actions/workflows/dtoverlaycheck.yml/badge.svg?branch=rpi-6.6.y)](https://github.com/raspberrypi/linux/actions/workflows/dtoverlaycheck.yml)




## CROSS_COMPILE on Ubuntu server
```console
KERNEL=kernel7l
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- bcm2711_defconfig
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- menuconfig
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- -j4 zImage modules dtbs
```

# Compile on Rasberry PI 64 bits

```console
KERNEL=kernel8
make bcm2711_defconfig
make menuconfig

sudo make Image modules dtbs
sudo make modules_install
sudo cp arch/arm64/boot/dts/broadcom/*.dtb /boot/
sudo cp arch/arm64/boot/dts/overlays/*.dtb* /boot/overlays/
sudo cp arch/arm64/boot/Image /boot/$KERNEL.img
ls -la /boot/$KERNEL.img

sudo dtc -@ -I dts -O dtb -o iris-kd070-panel.dtbo iris-kd070-panel.dts
```

# Compile on Rasberry PI 32 bits

```console
sudo apt install git bc bison flex libssl-dev make -y
sudo apt install libncurses5-dev -y 

git clone https://github.com/nutkondee/rpikernel.git
cd ~/rpikernel
KERNEL=kernel7l
make bcm2711_defconfig
make menuconfig

make -j4 zImage modules dtbs
sudo make modules_install
sudo cp arch/arm/boot/dts/*.dtb /boot/
sudo cp arch/arm/boot/dts/overlays/*.dtb* /boot/overlays/
sudo cp arch/arm/boot/dts/overlays/README /boot/overlays/
sudo cp arch/arm/boot/zImage /boot/$KERNEL.img
```



# 2024 versions

```console

sudo apt install git bc bison flex libssl-dev make -y
sudo apt install libncurses5-dev -y 

git clone https://github.com/nutkondee/rpikernel.git
cd ~/rpikernel
KERNEL=kernel7l
make bcm2711_defconfig
make menuconfig

make -j4 zImage modules dtbs
sudo make modules_install


sudo cp arch/arm/boot/dts/*.dtb /boot/firmware/
sudo cp arch/arm/boot/dts/overlays/*.dtb* /boot/firmware/overlays/
sudo cp arch/arm/boot/dts/overlays/README /boot/firmware/overlays/
sudo cp arch/arm/boot/zImage /boot/firmware/$KERNEL.img

```
