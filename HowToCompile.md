# Downloading the source code #
## Stable code ##
Download last version from http://code.google.com/p/cvblob/downloads/list.

## Latest code ##
You need **Subversion** (http://subversion.tigris.org).

Read only checkout:
> `svn checkout http://cvblob.googlecode.com/svn/trunk/ cvblob-read-only`

# Dependencies #
In order to compile cvBlob you need the following:
  * CMAKE (http://www.cmake.org)
  * OpenCV (http://opencvlibrary.sourceforge.net)

## Installation of dependencies in Debian type SO (Ubuntu,...) using apt ##
```
sudo apt-get install cmake libcv1 libcv-dev libcvaux-dev libcvaux1
```

## Installation of dependencies in SuSE using Yast ##
```
su -c "yast -i libopencv1 opencv opencv-debuginfo opencv-debugsource opencv-devel opencv-python cmake cmake-gui"
```

## Installation of dependencies in Red Hat/Fedora using yum ##
_Not tested._
```
su -c "yum install gcc gcc-c++ make cmake opencv-devel"
```

# Details #
In Linux, if you have installed the source in `$CVBLOB`, type in a console:
```
cd $CVBLOB
cmake
make
```

In Windows it must be as easy as in Linux (changing `make` for the equivalent in your system).

If problems, please read http://www.cmake.org/HTML/RunningCMake.html.