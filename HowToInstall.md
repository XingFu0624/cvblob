

# Dependencies #
In order to compile cvBlob you need the following:
  * [OpenCV](http://opencv.willowgarage.com)
  * [CMAKE](http://www.cmake.org) (optional, but highly recommended)

# Download #

## Stable version ##
Download last version from [download page](http://code.google.com/p/cvblob/downloads/list).

## Latest code ##
You need [Subversion](http://subversion.tigris.org).

Read only checkout:
```
svn checkout http://cvblob.googlecode.com/svn/trunk/ cvblob
```

# Compilation #

## Linux ##
If you have uncompressed the source in `$CVBLOB`, type in a console:
```
cd $CVBLOB
cmake .
make
```

To indicate where OpenCV is, use `OpenCV_DIR` variable:
```
cmake . -DOpenCV_DIR=<path_to_OpenCV>
```

# Installation #

## Linux ##
If you have compiled the source in `$CVBLOBBIN`, type in a console:
```
cd $CVBLOBBIN
sudo make install
```

To change the destination path use `CMAKE_INSTALL_PREFIX` when execute CMAKE:
```
cmake . -DCMAKE_INSTALL_PREFIX=<installation_path>
```