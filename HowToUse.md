# 1 In your source code #
Put
```
#include "cvblob.h"
```
in your code.

Also, in recent versions of cvBlob, all functions are inside a namespace named `cvb`. So, perhaps you want to include this line in your code:
```
using namespace cvb;
```

# 2 Compile your programs #

## g++ ##
If you have compiled and installed cvBlob (see HowToInstall):
```
g++ `pkg-config opencv cvblob --cflags --libs` sample.cpp -o sample
```