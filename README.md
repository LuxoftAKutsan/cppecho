[![Build Status](https://travis-ci.org/malirod/cppecho.svg?branch=master)](https://travis-ci.org/malirod/cppecho)

#cppecho
Echo server in c++

##Platform

Ubuntu 16.04: Clang 3.8, GCC 5.4

C++11 Standard is used.

##Setup

###Install Boost

####Use pre-build Boost lib

Use the following repository: https://github.com/malirod/boost-bin

Use appropriate branch. Branch name containts info about used env and options to build Boost.

E.g.

https://github.com/malirod/boost-bin/tree/boost-1.61-ubuntu-16.04-x64-clang-5.8-release-c++11-static-multi

####Build Boost manually from sources
If pre-build version doesn't fit your needs (OS, compiler etc) then build Boost manually.

Download and unzip to some dir (e.g. `~/libs/boost_1_61_0`) latest stable version from [Boost site](http://www.boost.org/).

Go the unzipped directory and run commands

```
./bootstrap.sh --prefix=./build
./b2 --with=all -j2 install
```

####Set environment variable
Set env pointing to the boost install dir (in ~/.profile or ~/.bashrc)

`export BOOST_HOME=~/libs/boost_1_61_0/build`

Restart terminal, or reload config with `source ~/.profile` (`source ~/.bashrc`)

##Setup git hook

Run `python infrastructure/tools/install_hooks.py`

This will allow to perform some code checks locally before posting changes to server.

##Install pylint - python checker

`sudo apt-get install pylint`

##Build

####Build commands
- `build` - debug build
- `build_all` - relase and debug build
- `build_debug` - debug build
- `build_releas` - release build

Sample. In the project root call

`./waf configure build_all`

To build specific target use `--targets` option during configuration

Sample

`./waf configure --targets=testrunner`

List all available targets with `./waf list`

Clang is used by defaul. Fallback to GCC if Clang not found. To use GCC call

`CXX=g++ ./waf configure`

###Build with sanitizers (clang)

Use the following option for configuration `--sanitize`. Applicable to debug build only. Known values are:

- `asan`: address
- `tsan`: thread
- `msan`: memory
- `ubsan`: undefined behaviour

Example

```
./waf configure --logger=log4cplus --sanitize=asan
./waf build_debug -v
ASAN_OPTIONS="detect_leaks=1" ./build/debug/testrunner
```

##Run

Run from project root. It's expected that config is located in the project root.

`build/debug/testrunner`
