==================================================================
Quick configure, build and install hints for Trilinos
==================================================================

:Contact: trilinos-framework@software.sandia.gov

This document is intended to be a very concise set of examples of how to
configure, build, install, and build downstream code against Trilinos. The
intended audience is those who need a quick refresher on Trilinos CMake build
system or those wanting a quick install without worrying about all the
features and options that are available.  For a more in-depth document on what
features and options are available and how to use them, see the document:

  https://trilinos.org/docs/files/TrilinosBuildReference.html

.. sectnum::

.. contents::


Requirements
============

* CMake 3.23.0 or newer
* C and C++ compiler
* Optionally a Fortran compiler
* Optionally an installation of MPI

Test system
============
* Macbook Air M2, 2022 (aarch64 architecture)
* Ubuntu 22.04.2 LTS (jammy) based on UTM Virtual Machine

Instructions
============

Following are a few examples of simple configurations for Trilinos. Anything in
<> should be replaced with the appropriate path or value and excluding the <>.

It is recommended that you put your configure options in a script (e..g
``do-configure``) so you can repeat the configure if necessary.

Note: all examples assume a unix like command line and the CMake Makefile
Generator.

Download
-----------------------------------------------
1. Download  trilinos from GitHub. Unpack it.

2. Put the folder TriBITS outside the trilinos folder.

3. Create a subfolder where you want to build trilinos. For example, <path to trilinos unpacked folder>/build

4. Create the target folder like `.../NetBeans_Project/MyProject/lib/trilinos`. Otherwise, the "make" will not happen.

5. Go to the build folder and execute the command cmake listed below.

non-MPI
-----------------------------------------------

::

  cmake \
  -DCMAKE_C_COMPILER=/usr/bin/gcc \
  -DCMAKE_CXX_COMPILER=/usr/bin/g++ \
  -DCMAKE_Fortran_COMPILER=/usr/bin/gfortran \
  -DTPL_ENABLE_MPI=OFF \
  -DBUILD_SHARED_LIBS=ON \
  -DTrilinos_ENABLE_AztecOO=ON \
  -DTrilinos_ENABLE_Epetra=ON \
  -DTrilinos_ENABLE_EpetraExt=ON \
  -Dtrilinos_ENABLE_Gtest=ON \
  -Dtrilinos_ENABLE_Kokkos=ON \
  -Dtrilinos_ENABLE_Teuchos=ON \
  -Dtrilinos_ENABLE_Triutils=ON \
  -DTrilinos_ENABLE_FLOAT=ON \
  -DCMAKE_INSTALL_PREFIX=/Home/Venus/Folders/NetBeans_Project/MyProject/lib/trilinos \
  -DTrilinos_TRIBITS_DIR:STRING=/Home/Venus/Folders/Trilinos-source-13.0.0/TriBITS/tribits \
  -DTrilinos_TRIBITS_PACKAGE_USE_TRIBITS_DIR=TRUE \
  /Home/Venus/Folders/Trilinos-source-13.0.0
  
  make install

MPI
-----------------------------------------------

::

  cmake \
  -DCMAKE_C_COMPILER=/usr/bin/mpicc \
  -DCMAKE_CXX_COMPILER=/usr/bin/mpicxx \
  -DCMAKE_Fortran_COMPILER=/usr/bin/mpif77 \
  -DTPL_ENABLE_MPI=ON \
  -DBUILD_SHARED_LIBS=ON \
  -DTrilinos_ENABLE_AztecOO=ON \
  -DTrilinos_ENABLE_Epetra=ON \
  -DTrilinos_ENABLE_EpetraExt=ON \
  -Dtrilinos_ENABLE_Gtest=ON \
  -Dtrilinos_ENABLE_Kokkos=ON \
  -Dtrilinos_ENABLE_Teuchos=ON \
  -Dtrilinos_ENABLE_Triutils=ON \
  -DTrilinos_ENABLE_FLOAT=ON \
  -DCMAKE_INSTALL_PREFIX=/Home/Venus/Folders/NetBeans_Project/MyProject/lib/trilinos-mpi \
  -DTrilinos_TRIBITS_DIR:STRING=/Home/Venus/Folders/Trilinos-source-13.0.0/TriBITS/tribits \
  -DTrilinos_TRIBITS_PACKAGE_USE_TRIBITS_DIR=TRUE \
  /Home/Venus/Folders/Trilinos-source-13.0.0
  
  make install


Useful Options
==============

To generate Ninja build files (Ninja 1.10+) instead of Makefiles use::

  -GNinja

To use shared libraries (much smaller executables and faster linking) use::

  -DBUILD_SHARED_LIBS=ON

To enable support for the ``float`` scalar type use::

  -DTrilinos_ENABLE_FLOAT=ON

To enable support for ``std::complex<T>`` scalar types use::

  -DTrilinos_ENABLE_COMPLEX=ON

To disable Fortran use the following::

  -DTrilinos_ENABLE_Fortran=OFF

To enable a package::

  -DTrilinos_ENABLE_<package name>=ON

To get the list of packages that can be enabled, run::

  cmake <path to Trilinos source> 2>&1 \
    | grep "Final set of non-enabled SE packages"

To enable tests::

  -DTrilinos_ENABLE_TESTS=ON


Building against installed Trilinos
===================================

For information on how to build against an installation of Trilinos, see
`demos/simpleBuildAgainstTrilinos`_

.. _demos/simpleBuildAgainstTrilinos: demos/simpleBuildAgainstTrilinos/README.md


Support for Different Compilers/MPIs
====================================

Trilinos tests with all Compiler/MPI combinations listed at:

  https://github.com/trilinos/Trilinos/wiki/Pull-Request-Testing-Interface

Compilers/MPIs that are not part of our automated process will not receive support.
We are happy to accept Pull Requests enhancing support for other compilers/MPIs as
needed by our customers, with the understanding that said configurations cannot be
guaranteed to work.
