---
layout: post
title: CMake Project build.sh
---

There is a shell script which I commonly copy into CMake-based projects.

I thought it'd be useful to just document it as part of the blog:
```
#!/bin/bash

set -euxo pipefail

# Create build dir.
mkdir -p build && cd build

# CMake configure.
CMAKE_ARGS='
 -DCMAKE_BUILD_TYPE="Release"
 -DBUILD_TESTING=ON
'

# CMake build & install.
if [ $# -eq 0 ]
then
    cmake $CMAKE_ARGS ..
    cmake --build . -- VERBOSE=1 -j16 all test
else
    cmake $CMAKE_ARGS -DCMAKE_INSTALL_PREFIX=$1 ..
    cmake --build . -- VERBOSE=1 -j16 all test install
fi
```

I've usually named this file `build.sh`, and included it as part of the project's `.gitignore`.
