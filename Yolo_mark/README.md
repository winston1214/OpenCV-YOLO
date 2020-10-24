# Yolo_mark

Supported both: OpenCV 2.x and OpenCV 3.x

## My working environment
- Ubuntu 18.04.5

- virtual env

- opencv3.2

- CUDA 10.2


## Install OpenCV 3.2 <a href = 'https://bigdata-analyst.tistory.com/220'>See Kor ver </a>

- Install basic package 
```
$ sudo apt-get update
$ sudo apt-get upgrade
$ sudo apt-get install g++
$ sudo apt-get install build-essential cmake
$ sudo apt-get install pkg-config
$ sudo apt-get install libjpeg-dev libpng-dev
$ sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libxvidcore-dev libx264-dev libxine2-dev
$ sudo apt-get install lib41-dev v4l-utils
$ sudo apt-get install libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev 
$ sudo apt-get install libgtk2.0-dev
$ sudo apt-get install mesa-utils libgl1-mesa-dri libgtkgl2.0-dev libgtkglext1-dev  
$ sudo apt-get install libatlas-base-dev gfortran libeigen3-dev
$ sudo apt-get install python2.7-dev python3-dev python-numpy python3-numpy
```
- Setting path & Installation

```
$ makdir opencv
$ cd opencv
$ wget -O opencv.zip https://github.com/Itseez/opencv/archive/3.2.0.zip
$ Unzip opencv.zip
$ Wget –O opencv_contrib.zip https://github.com/Itseez/opencv_contrib/archive/3.2.0.zip
$ Unzip opencv_contrib.zip
```

```
$ cd opencv-3.2.0
$ mkdir build
$ cd build
```
```
$ cmake \
-D CMAKE_BUILD_TYPE=RELEASE \
-D CMAKE_INSTALL_PREFIX=/usr/local \
-D WITH_TBB=OFF \
-D WITH_IPP=OFF \
-D WITH_1394=OFF\
-D BUILD_WITH_DEBUG_INFO=OFF \
-D BUILD_DOCS=OFF \
-D INSTALL_C_EXAMPLES=ON \
-D INSTALL_PYTHON_EXAMPLES=ON \
-D BUILD_EXAMPLES=OFF \
-D BUILD_TESTS=OFF \
-D BUILD_PERF_TESTS=OFF \
-D ENABLE_NEON=ON \
-D WITH_QT=OFF \
-D WITH_OPENGL=ON \
-D WITH_CUDA=OFF \
-D WITH_CUDNN=ON \
-D OPENCV_DNN_CUDA=ON \
-D CUDA_ARCH_BIN=7.5 \
-D OPENCV_EXTRA_MODULES_PATH=../../opencv_contrib-3.2.0/modules \
-D WITH_V4L=ON \
-D WITH_FFMPEG=ON \
-D WITH_XINE=ON \
-D BUILD_NEW_PYTHON_SUPPORT=ON \
-D PYTHON_INCLUDE_DIR=/usr/include/python2.7\
-D BUILD_LIBPROTOBUF_FROM_SOURCES=ON -D PYTHON_INCLUDE_DIR2=/usr/include/x86_64-linux-gnu/python2.7 -D PYTHON_LIBRARY=/usr/lib/x86_64-linux-gnu/libpython2.7.so ../ 2>&1 ../../opencv-3.2.0/ | tee cmake_messages.txt
```
**if you occur "cmake cuda error", you should set "WITH_CUDA=OFF"**
```
$ cat /proc/cpuinfo | grep processor | wc –l # Check number of available cpu core
$ sudo make –j12 # The number is the number of cores you will be able to use
$ sudo make install
```
**if you occur "make error", you should set "WITH_QT=OFF"**

- Check Installation
```
$ pkg-config --modversion opencv # check opencv version
$ pkg-config –libs –cflags opencv
```

## YOLO_MARK

- Install YOLO_MARKER
```
$ git clone https://github.com/AlexeyAB/Yolo_mark
$ cd Yolo_mark
$ cmake .
$ chmod u+x ./linux_mark.sh
```
- Excute
```
$ ./linux_mark.sh
```
- Output
![Output](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbehpIr%2FbtqwgAEnP8j%2FGM7tvrKFFeO2a7nrCq5631%2Fimg.png)


- Setting
1. After checking that the image appears, press ESC and exit the sample data.
2. Afterwards, clear all sample folders in the Yolo_mark/x64/Release/data/img.
3. And put all the images to label into the folder.
4. Go to the path Yolo_mark/x64/Release/data
5. ```$ vi obj.data```
![obj.data](https://user-images.githubusercontent.com/47775179/97078857-2a5b5c00-162a-11eb-9b98-14a69d8f5827.png)
You can modify it as you want.

6. ```$ vi obj.names```
![obj.names](https://user-images.githubusercontent.com/47775179/97078866-3e9f5900-162a-11eb-94c5-656f9ba45663.png)
The obj.names file is modified as well.

- Labeling
```
$ cd ~/Yolo_mark
$ ./linux_mark.sh```
```
- Operating Method

Draw a bounding box through a mouse drag.

Generate a number for a class with a numeric pad

If you drew it incorrectly, click the bounding box you created, and then click R.

For more help, press H.


- Finish
Press ctrl c after input.

The labeled coordinates are stored in both the **Yolo_mark/x64/Release/data/img** file.

Changes will be required depending on future yolo model work

