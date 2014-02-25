Makefile dependency detection for Fortran
=========================================

[![Build Status](https://travis-ci.org/ScottWales/fortran-build-testing.png?branch=master)](https://travis-ci.org/ScottWales/fortran-build-testing)

Fortran's module system makes it somewhat complicated to handle dependencies
between different files when building. To compile a source file you need to
have available all of the `.mod` files that the source file imports, which are
generated by compiling the source files for those modules and so on.

Since these dependencies are already enumerated in the source code it doesn't
make much sense to manually list them in the project's Makefile. Here we
demonstrate using a helper program to automatically generate the dependencies -
any Fortran files under the `src/` directory will be scanned for what modules
they use & provide, then this information is used to produce a dependency tree.

To build:
=========

The build system supports incremental and parallel builds. To compile all
PROGRAMs and tests run:

    $ make

Note that pFunit requires some Fortran 2003 features not available in older
versions of gfortran. Testing is done using gfortran-4.8, to install on Ubuntu:

    $ sudo apt-add-repository ppa:ubuntu-toolchain-r/test
    $ sudo apt-get update
    $ sudo apt-get install gfortran-4.8
    $ export FC=gfortran-4.8
    $ export OMPI_FC=$FC

Tests
=====

Tests use [pFunit](http://sourceforge.net/projects/pfunit) & require the PFUNIT environment variable to be set.
Tests are run automatically when building the program, or run

    $ make check

Note that you should use the `pfunit_2.1.0` branch, and it will require gfortran 4.8 or later (see http://sourceforge.net/p/pfunit/mailman/message/31811969/)
