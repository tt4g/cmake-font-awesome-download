# Overview

Download Font Awesome from GitHub release.

## Usage

Clone this repository or copy `cmake/FontAwesome5Download.cmake`,
and `include(${REPOSITORY}/cmake/FontAwesome5Download.cmake)` in `CMakeLists.txt`.

### Functions

See `cmake/FontAwesome5Download.cmake`.

## Test

```bash
$ mkdir build
$ cd build
$ ctest ../test
$ cmake --build .
$ ctest -C Debug
```
