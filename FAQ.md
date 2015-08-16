

# 1 Introduction #

## 1.1 Are cvBlob and cvBlobLib the same? ##

No.

[cvBlobLib](http://opencvlibrary.sourceforge.net/cvBlobsLib) is a completely different library for the same purpose. In fact, I began to use it but it didn't work for me so I developed my own library as part of a bigger project.

Certainly, it was a bad idea calling my library cvBlob. In the beginning, my library was private so I called as I thought it would be more correct inside the whole project.

## 1.2 Is there any documentation of cvBlob? ##

Not yet. But the code is being documented using [Doxygen](http://www.doxygen.org).

You need to download version 0.9.8 (or newer) of the code. Then execute `doxygen` where `Doxyfile` file is. Documentation generated will be in `doc` directory in two formats: `html` and `xml`.

Also, you can [download](http://code.google.com/p/cvblob/downloads/list) the `doc` package.

I'm trying to put this documentation in the wiki.

Further, you have some sample code in "test" and "samples" directories in the cvBlob package.

## 1.3 What is the labeling algorithm that cvBlob uses? ##

From version 0.10.0 the labeling algorithm is one based on the paper of Fu Chang, Chun-Jen Chen and Chi-Jen Lu called "A linear-time component-labeling algorithm using contour tracing technique". This algorithm runs twice faster than previous versions of cvBlob, and obtains external and internal contours of each blob in the same pass. Also, it labels 8-connectivity components (unlike the previous algorithm which detects only 4-connected components). Also, the blobs identifications are now incremental.

## 1.4 What's wrong with the tracking algorithm? ##

In older versions of cvBlob the tracking was unusable. It had bugs and the algorithm needed to be fixed.

The tracking code was rewritten in version 0.9.13 and now it works a lot better, but there is some bugs yet.

Keep in mind that the tracking algorithm in cvBlob is **very** simple. It's only for testing or fast prototyping.

## 1.5 What is the tracking algorithm that cvBlob uses? ##

In the beginning, my tracking algorithm was based on the _high level
tracking_ of the paper of A. Senior, A. Hampapur, Y-L Tian, L. Brown, S. Pankanti and R. Bolle called ["Appearance Models for Occlusion Handling"](http://www.research.ibm.com/peoplevision/PETS2001.pdf).

But then I rewrote it again and again.

As I said before, the tracking algorithm it's only for fast prototyping. It is not intended for serious projects. cvBlob's tracking algorithm only takes into account the position and bounding box of the blobs. But a good tracking algorithm need to consider:

  * The history of the positions of the blob (actually this could be added to cvBlob, as a _Kalman filter_, or something like that... maybe in the future).
  * Appearance models (this is outside the bounds of the project): this can be color histograms, shape features,...

This two points depends on the problem that you need to approach, and it's difficult to give a general solution.

## 1.6 Why cvBlob is so slow? ##

There are some reports of cvBlob running quite slow when compiled with Visual Studio. In the same Windows machine, running [test\_random](http://code.google.com/p/cvblob/source/browse/trunk/test/test_random.cpp), with Visual Studio it gives elapse times of over 1000 ms, but when compiled with [MinGW](http://www.mingw.org/) the elapse time dropped about 20 ms. No debug mode and optimization on. I don't know the why of such a huge difference.

So, as far as I know, cvBlob has no significant problem with the speed.

# 2 Compiling #

## 2.1 Is [CMAKE](http://www.cmake.org) obligatory to compile cvBlob? ##

No, it isn't.

## 2.2 How can I use cvBlob? ##

Firstly, you need a compiled version of cvBlob. You can:
  1. Compile and install cvBlob using CMAKE (read HowToInstall).
  1. Set up yourself a project that build a library and add cvBlob files (`*.h` and `*.cpp` in `cvBlob` directory), what is exactly what CMAKE does automatically.

Then set up your project in order to link with the generated library and find `cvblob.h` file.

## 2.3 When I build cvBlob, the compiler returns a list with a lot of warnings, is it normal? ##

Yes. I'm working for fix all this warnings. Anyway, they do not affect in the using of cvBlob.

## 2.4 How can I compile a simple program with gcc/g++ that uses cvBlob? ##

I usually use this `Makefile` in Kubuntu (considering that cvBlob is compiled and installed normally):

```
sample:      sample.cpp
        g++ `pkg-config opencv cvblob --cflags --libs` sample.cpp -o sample
```

## 2.5 When starting my program, I get the message "`error while loading shared libraries: libcvblob.so: cannot open shared object file: No such file or directory`". What's wrong? ##

Try running `ldconfig`.

# 3 Using the library #

## 3.1 How do I get the blobs of an image? ##

I assume that you have cvBlob compiled and you have in your source code this line:

```
#include <cvblob.h>
```

In recent versions of cvBlob all functions and types are in the namespace called `cvb`, so perhaps you want to include this line in your code:

```
using namespace cvb;
```

Firstly, cvBlob works with black and white images, so, you need to convert your color/gray image to a binary one.

If you have a one channel gray scale image you can just use `cvThreshold` function, like this:

```
cvThreshold(img, img, 100, 200, CV_THRESH_BINARY);
```

In the other hand, if your image is a multiple channel image (a RGB image, for example) you must reduce the number of channels to one. You can combine the channels in any way you find useful or simply take one of the channels. This depends on the kind of application you want. To take a channel you can use `cvSplit`:

```
IplImage *chB=cvCreateImage(cvGetSize(img), 8, 1);
cvSplit(img, chB, NULL, NULL, NULL);
```

This way you get the blue channel of the image in `chB`. Remember, when you have a one channel image you need to binarize it, if there was not before.

Also, you can generate a gray image from the RGB one:

```
IplImage *gray = cvCreateImage(cvGetSize(img), IPL_DEPTH_8U, 1);
cvCvtColor(img, gray, CV_BGR2GRAY);
cvThreshold(gray, gray, 150, 255, CV_THRESH_BINARY);
```

So, you have a one channel binary image. Then you can get the blobs just like that:

```
IplImage *labelImg=cvCreateImage(cvGetSize(gray), IPL_DEPTH_LABEL, 1);
CvBlobs blobs;
unsigned int result=cvLabel(gray, labelImg, blobs);
```

Now you can simply render the blobs in the original image:

```
cvRenderBlobs(labelImg, blobs, img, img);
```

Or iterate over the blobs to obtain some information (area and centroid coordinates):

```
for (CvBlobs::const_iterator it=blobs.begin(); it!=blobs.end(); ++it)
{
  cout << "Blob #" << it->second->label << ": Area=" << it->second->area << ", Centroid=(" << it->second->centroid.x << ", " << it->second->centroid.y << ")" << endl;
}
```

## 3.2 How can I track red objects? ##

Look at [red\_object\_tracking](http://code.google.com/p/cvblob/source/browse/trunk/samples/red_object_tracking.cpp) sample in the cvBlob package (since 0.9.14 version).

You can see a [video](http://www.youtube.com/watch?v=0dMGDzFYXVY) of the result.

Also, check out the tutorial [Color-based Blob Detection](http://www.shervinemami.info/blobs.html) of **Shervin Emami**.

## 3.3 How are cvBlob/cvBlobs, cvTrack/cvTracks different? ##

I use the sufix '-s' to indicate "list of...".

So, cvBlobs is a list of cvBlob. And cvTracks is a list of cvTrack.

## 3.4 How can I save the image of a blob? ##

From version 0.10.3 there is a new function called `cvSaveImageBlob`. For an example of use look at [red\_object\_tracking](http://code.google.com/p/cvblob/source/browse/trunk/samples/red_object_tracking.cpp).

## 3.5 How can I obtain a list of the blobs ordered by the Y coordinate of the centroid? ##

As `CvBlobs` type is a `map` of C++ STL (Standard Template Library), you can use a lot of standard function on it. In this case, to convert CvBlobs to a `vector` of blobs, and then order it by the Y coordinate of their centroids you can do this:

```
bool cmpY(const pair<CvLabel, CvBlob*>  &p1, const pair<CvLabel, CvBlob*> &p2)
{
  return p1.second->centroid.y < p2.second->centroid.y;
}

int main()
{ 
//...
  CvBlobs blobs;
  unsigned int result = cvLabel(binaryImg, labelImg, blobs);

  vector< pair<CvLabel, CvBlob*> > blobList;
  copy(blobs.begin(), blobs.end(), back_inserter(blobList));

  sort(blobList.begin(), blobList.end(), cmpY);
  for (int i=0; i<blobList.size(); i++)
  {
    // This will print: [LABEL] -> BLOB_DATA
    cout << "[" << blobList[i].first << "] -> " << (*blobList[i].second) << endl;
  }
//...
}
```

# 4 Miscellanea #

## 4.1 Who is using cvBlob? ##

There are a lot of people using this library: students, researchers, software companies, etc.

I want to maintain a list of projects that are using cvBlob in any way, so if you are a developer of one of this projects, tell me. Send me an URL to the webpage of the project or to a video of your program.

I have a list on YouTube with videos of people using cvBlob: [cvBlob Video List](http://www.youtube.com/user/grendelccl#grid/user/39264608ACB2113E).

## 4.2 How can I cite cvBlob? ##

It's important that you cite this library if you are using it in your research projects. This way your methods are more reproducible and gain in credibility.

Here is the the [BibTex](http://www.bibtex.org/) entry for citing cvBlob:
```
@misc{cvblob,
      title = {{cvBlob}},
      url = {http://cvblob.googlecode.com},
      howpublished = {http://cvblob.googlecode.com},
      author = {Crist\'obal Carnero Li\~n\'an},
}
```

## 4.3 How can I contribute? ##

Several ways:

  * Make a [donation](https://www.paypal.com/cgi-bin/webscr?cmd=_donations&business=UN82U3BVRPQRC&lc=ES&item_name=cvBlob&currency_code=EUR&bn=PP%2dDonationsBF%3abtn_donate_LG%2egif%3aNonHosted) or a [micro-donation](https://flattr.com/thing/511229).
  * Report [bugs](http://code.google.com/p/cvblob/issues).
  * Write documentation, HOWTOs, tutorials,... about using the library or simply how to compile or use it in the environment you use.
  * Send code: new functionality, patches, tests or sample code.
  * Mention cvBlob in your blog, cite in your work, link in your page,...
  * Hire me :)

Thanks!