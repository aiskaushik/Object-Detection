![Example Image](https://github.com/aiskaushi/Object-Detection/blob/main/image1.jpg)

# Object-Detection using Raspberry Pi

Object and Animal Recognition With Raspberry Pi and OpenCV

## Table of Contents
- [Raspberry pi -4 OS Installation](#installation-Basic-and-Initial-Requirements)
  - [Download armhf-image](#download-armhf-image)
  - [Check Raspberry Pi OS Size](#check-raspberry-pi-os-size)
  - [Cutting the Fat from Raspberry Pi OS](#cutting-the-fat-from-raspberry-pi-os)
- [Prepare System for Installation](#prepare-system-for-installation)
  - [Remove Unnecessary Files](#remove-unnecessary-files)
- [Setting Up OpenCV for Object Detection](#setting-up-opencv-for-object-detection)
  - [Update & Upgrade Raspberry Pi-4](#update--upgrade-raspberry-pi-4)
  - [Change CONF_SWAPSIZE](#change-conf-swapsize)
  - [Install Necessary Packages](#install-necessary-packages)
  - [Download and Unzip OpenCV](#download-and-unzip-opencv)
  - [Build and Install OpenCV](#build-and-install-opencv)
  - [Reboot](#reboot)

---

## Installation & Basic and Initial Requirements

1. Download the link for armhf-image:
    ```bash
    https://downloads.raspberrypi.org/raspios_armhf/images/raspios_armhf-2021-05-28/
    ```

2. Check the current size of the Raspberry Pi OS Install:
    ```bash
    df -h /
    ```

3. Cutting the Fat from Raspberry Pi OS:
    ```bash
    dpkg-query -Wf '${Installed-Size}\t${Package}\n' | sort -n -r | head -n 20
    ```

---

## First, let’s prepare the system for the installation.

4. Remove unnecessary files:
    ```bash
    sudo apt-get -y purge wolfram-engine
    sudo apt-get -y purge libreoffice*
    sudo apt-get -y clean
    sudo apt-get -y autoremove
    ```

---

## Setting Up OpenCV for Object Detection

5. Update & upgrade your Raspberry Pi-4:
    ```bash
    sudo apt-get update && sudo apt-get upgrade
    ```

6. Change the number on `CONF_SWAPSIZE = 100` to `CONF_SWAPSIZE=2048`:
    ```bash
    sudo nano /etc/dphys-swapfile
    ```

7. Install necessary packages:
    ```bash
    sudo apt-get install build-essential cmake pkg-config
    sudo apt-get install libjpeg-dev libtiff5-dev libjasper-dev libpng12-dev
    sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev
    sudo apt-get install libxvidcore-dev libx264-dev
    sudo apt-get install libgtk2.0-dev libgtk-3-dev
    sudo apt-get install libatlas-base-dev gfortran
    sudo pip3 install numpy
    ```

8. Download and unzip OpenCV:
    ```bash
    wget -O opencv.zip https://github.com/opencv/opencv/archive/4.4.1.zip
    wget -O opencv_contrib.zip https://github.com/opencv/opencv_contrib/archive/4.4.1.zip
    unzip opencv.zip
    unzip opencv_contrib.zip
    ```

9. Build and install OpenCV:
    ```bash
    cd ~/opencv-4.4.0/
    mkdir build
    cd build
    cmake -D CMAKE_BUILD_TYPE=RELEASE \
        -D CMAKE_INSTALL_PREFIX=/usr/local \
        -D INSTALL_PYTHON_EXAMPLES=ON \
        -D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib-4.4.0/modules \
        -D BUILD_EXAMPLES=ON ..
    make -j $(nproc) # This 'make' command will take over an hour to install and there will be no indication of how much longer it will take.
    sudo make install && sudo ldconfig
10. Change the number on `CONF_SWAPSIZE = 2048` to `CONF_SWAPSIZE= 100`:
    ```bash
    sudo nano /etc/dphys-swapfile  
    sudo reboot
    ```

---

Thank You for following steps correctly.
