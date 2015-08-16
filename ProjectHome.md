## Description ##
**cvBlob** is a library for computer vision to detect connected regions in binary digital images. cvBlob performs [connected component analysis](http://en.wikipedia.org/wiki/Connected_Component_Labeling) (also known as _labeling_) and features extraction.

[![](https://www.paypal.com/en_US/i/btn/btn_donate_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_donations&business=UN82U3BVRPQRC&lc=ES&item_name=cvBlob&currency_code=EUR&bn=PP%2dDonationsBF%3abtn_donate_LG%2egif%3aNonHosted) <wiki:gadget border="0" url="http://stefansundin.com/stuff/flattr/google-project-hosting.xml" width="55" height="62" up\_uid="grendel.ccl" up\_title="cvBlob" up\_desc="Blob library for OpenCV" up\_tags="blob, opencv, computer vision" up\_url="http://cvblob.googlecode.com" />

## Features ##
  * Binary image labeling.
  * Features extraction and render: blob orientation, centroid, contours, color,...
  * Contours functions.
  * Basic blob tracking.
  * Interface similar to OpenCV.

## News ##
  * 25/05/2012: Version 0.10.4 released: bugs fixed.
  * 04/01/2011: Version 0.10.3 released: `cvSaveImageBlob` function, bugs fixed, compilation and installation improved.
  * 24/09/2010: Version 0.10.2 released: new functions and bugs fixed.
  * 27/05/2010: Version 0.10.1 released: New function `cvWriteContourPolygonCSV`. Memory-leaks fixed.
  * 13/04/2010: Version 0.10.0 released!!! New labeling algorithm, more than twice faster. Internal contours. Blob color mean. And something more...
  * 07/04/2010: Version 0.9.15 released: minor bug fixed.
  * 10/03/2010: Version 0.9.14 released: sample program (red object tracking) and new function: `cvGetLabel`. This can be the last release of the 0.9 branch. New labeling algorithm in the next version.
  * 18/01/2010: Version 0.9.13 released: new contours functions, tracking rewritten. IMPORTANT: this version use now namespace `cvb`.
  * 12/14/2009: Version 0.9.12 released: new contours functions and memory-leaks fixed.
  * 10/07/2009: Version 0.9.11 released: error handling OpenCV style and bug fixed.
  * 09/30/2009: Version 0.9.10 released: contours functions and bugs fixed.
  * 09/23/2009: Version 0.9.9 released: ROI and very basic tracking.
  * [...](History.md)

## Screenshots and videos ##

### Basic test ###
| ![http://cvblob.googlecode.com/svn/wiki/Images/test_screenshot.png](http://cvblob.googlecode.com/svn/wiki/Images/test_screenshot.png) |
|:--------------------------------------------------------------------------------------------------------------------------------------|

### Red object tracking ###
| <a href='http://www.youtube.com/watch?feature=player_embedded&v=0dMGDzFYXVY' target='_blank'><img src='http://img.youtube.com/vi/0dMGDzFYXVY/0.jpg' width='425' height=344 /></a> |
|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|

&lt;wiki:gadget url="http://www.ohloh.net/p/104510/widgets/project\_users.xml?style=blue" height="100" border="0"/&gt;