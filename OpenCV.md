# Installation #

**Warning: this is not complete!**

Instructions for installation of OpenCV in Ubuntu (Lucid):

```
sudo aptitude install cmake build-essential libgtk2.0-dev libopenexr-dev libavcodec-dev libavformat-dev libavutil-dev libswscale-dev libdc1394-22-dev libxine-dev python-dev python-numpy swig
cd ~/src
svn co https://code.ros.org/svn/opencv/trunk opencv
cd opencv/opencv
mkdir release
cd release
cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/ -D BUILD_PYTHON_SUPPORT=ON ..
make
sudo make install
export LD_LIBRARY_PATH=~/src/opencv.svn/opencv/release/lib:$LD_LIBRARY_PATH
sudo ldconfig
```

References:
  * [OpenCV Installation Guide](http://opencv.willowgarage.com/wiki/InstallGuide)