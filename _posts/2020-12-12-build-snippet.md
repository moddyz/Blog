---
layout: post
title: CMake Project build.sh
---

There is a shell script which I commonly copy into the root of CMake-based projects, which can be `source`'ed.

I thought it'd be useful to just document it as part of the blog:
```bash
#!/bin/bash

set -euxo pipefail

# Create build dir.
mkdir -p build && cd build

# CMake configure.
CMAKE_ARGS=\
\ -DCMAKE_BUILD_TYPE="Release"\
\ -DBUILD_TESTING=ON

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

Similarly, a `runtime.sh` exists to set-up runtime environment variables:
```bash
#!/bin/bash

INSTALL_ROOT=/apps/ProjectEuler
appendEnv LD_LIBRARY_PATH ${INSTALL_ROOT}/lib
echo $INSTALL_ROOT
```

See [Poor man's environment variable management](https://moddyz.github.io/Blog/2020/10/04/env-var-management.html) for the `appendEnv` implementation.
