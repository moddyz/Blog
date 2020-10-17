---
layout: post
title: Onboarding Github Actions
---

Been integrating GitHub Actions workflows into various projects the past two weeks. 

So far - it's been a pleasant experience!  Huge fan of the integrated UI - and the slick job view.

One independent recipe that I've been deploying to C++ projects is the clang-format check:
```
# Run automated code formatting checks.
check-code-formatting:
  name: "Check C++ code formatting"
  runs-on: ubuntu-18.04 
  steps:
    - name: Install clang-format
      run: sudo apt-get install clang-format-10
    - uses: actions/checkout@v2
    - name: Run clang-format on source code
      run: |
        find . \
          -name ".git" -prune -o \
          -name "*.cpp" -type f -exec clang-format -i --verbose {} + -o \
          -name "*.h" -type f -exec clang-format -i --verbose {} +
    - name: Check for source differences
      run: |
        set +e
        git diff --color
        git diff-index --quiet HEAD --; EXIT_CODE=$?
        set -e
        if [ $EXIT_CODE -ne 0 ]; then echo "C++ code formatting check failed.  Please run clang-format on *.h and *.cpp, then push your changes."; fi
        exit $EXIT_CODE
```

This job _fails_ when the source tree is not formatted to standard - then highlights the code differences.
