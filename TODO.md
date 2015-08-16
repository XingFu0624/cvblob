# Features to implement for 1.0 release #
  * ~~New labeling algorithm. Faster and with internal contour tracing.~~ **Done** (since version 0.10.0).
  * ~~Blob mean color.~~ **Done** (since version 0.10.0).
  * Color histogram in blob.
  * Python interface.
  * Extensive documentation, tutorials and samples.

# Others #
  * C++ interface as OpenCV has.
  * Compatibility with OpenCV types:
    * Contours.
  * Release binaries:
    * Linux: `.rpm`, `.deb`
    * Win32: DLLs

# Optimizations #
  * Use `std::Vector.reserve` when possible.