---
layout: post
title: CMake Gems - add_subdirectories
---

Over half a year ago I started building a [CMake template project](https://github.com/moddyz/CMakeTemplate) for basing new C++ projects off of.

Overall it has been a time saver and it was fun learning the basics of the CMake.

One of my favorite macros is [add_subdirectories](https://github.com/moddyz/CMakeTemplate/blob/master/cmake/macros/Public.cmake#L400).

This one is easy to use in client code.  It simply calls add_subdirectory(...) on each subdirectory.  
It does expect a `CMakeLists.txt` to be to be available in each of the subdirectories.

Notably this scales well in root directories which host a collection of library or program subdirs. [See example](https://github.com/moddyz/RayTracingInOneWeekend/blob/master/src/CMakeLists.txt).

