SaC standard library
====================

[![build status](https://github.com/SacBase/Stdlib/workflows/Build%20On%20Changes/badge.svg)](https://github.com/SacBase/Stdlib/actions?query=workflow%3A"Build+On+Changes")
[![contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg)](https://github.com/SacBase/Stdlib/issues)

This repository consists of SaC modules with basic functionality like
arithmetic, stdio, etc; which together form the standard library of the SaC
language.

Build instructions
==================

To build the system one requires an operational
[CMake](https://cmake.org/) >= 3.3,
[Flex](http://flex.sourceforge.net/), and
[Bison](https://www.gnu.org/software/bison/).

An example on how to build the library:
```bash
$ cd Stdlib
$ git submodule init
$ git submodule update
$ mkdir build
$ cd build
$ cmake ..
$ make -j4  # you should have roughly 2GB per thread :-)
```

Additionally, if you forked this repository, you should fetch the tags:
```bash
$ git remote add upstream git@github.com:SacBase/Stdlib.git
$ git fetch --tags upstream
```

If you like you can also install the stdlib into `/usr/local` with `make
install`, but this is _unnecessary_ as `sac2c` will be able to find your stdlib
build automatically.
This is achieved through a file named `sac2crc.package.stdlib`
which is being placed in `~/.sac2crc/` and which contains the path to the place
where you build your stdlib.

**NOTE:**
*When pulling the latest commit, remember to run `git submodule update` or you
will be missing changes to the `cmake-common` repository.*

Variables that can be passed to CMake
=====================================

When running CMake it is possible to pass the following variables:

* `-DTARGETS=x;y;z` --- build stdlib for targets x, y and z.
  (Default is `seq;mt_pth`)
* `-DBUILDGENERIC=ON|OFF` --- build stdlib without using architecture specific
  optimisations (useful when creating distributable packages).
  (Default is `OFF`)
* `-DSAC2C_EXEC=/path/to/sac2c` --- specify `sac2c` executable directly.
  Otherwise CMake will try to find `sac2c` on yout PATH.
* `-DLINKSETSIZE=n` --- set `-linksetsize n` when calling `sac2c`.
  This option is responsible for the number of C functions that are put in a
  single C file when compiling a SaC program. The rule of thumb:
  * value `0` is the fastest time-wise but potentially results in a large memory
    consumption.
  * value `1` reduces the memory consumption to minimum, but significantly
    increases compilation time.
  (Default is `500`)
* `-DFULLTYPES=ON|OFF` --- add support for further types to the stdlib, such as
  `long` and `longlong`.
  (Default is `OFF`)
* `-DBUILD_EXT=ON|OFF` --- build extended stdlib.
  (See `cmake/source-core-ext.txt` for details)
  (Default is `ON`)

Continuous Integration
======================

We make use of Github Actions for our CI pipeline, building the standard library
on different systems anytime there is a pull request. Build will fail if there
are any compile-time warnings.

Currently we build on the following systems: `ubuntu-18.04` and `macos-11`.

Please look at `.github/workflows/` for more exact details on what we do.

Licensing
=========

This project is open-source, contributions are welcome!
Note that no warranty is given.

Please look at `LICENSE.txt` for further details.
