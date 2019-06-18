# cmake-font-awesome-download

[![Build Status](https://travis-ci.com/tt4g/cmake-font-awesome-download.svg?branch=master)](https://travis-ci.com/tt4g/cmake-font-awesome-download)

Download Font Awesome from the GitHub release page at CMake configure time.

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
