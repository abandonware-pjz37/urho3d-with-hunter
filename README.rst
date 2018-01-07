|travis| |appveyor|

.. |travis| image:: https://img.shields.io/travis/forexample/urho3d-with-hunter/master.svg?style=flat-square&label=Linux%20OSX%20Android%20iOS
  :target: https://travis-ci.org/forexample/urho3d-with-hunter/builds
  :alt: Travis CI

.. |appveyor| image:: https://img.shields.io/appveyor/ci/ruslo/urho3d-with-hunter/master.svg?style=flat-squre&label=Windows
  :target: https://ci.appveyor.com/project/ruslo/urho3d-with-hunter/history
  :alt: AppVeyor CI

Setup
-----

Check tools:

.. code-block:: none

  > which python3
  /usr/bin/python3

  > which cmake
  /usr/bin/cmake

Download Polly:

.. code-block:: none

  > git clone https://github.com/ruslo/polly
  > export PATH=`pwd`/polly/bin:${PATH}
  > which polly.py
  /.../polly/bin/polly.py

Polly is a collection of toolchains. Python script ``polly.py`` is just a wrapper
for CMake commands and is not a requirement. E.g. you can do:

.. code-block:: none

  > cmake -H. -B_builds/gcc -DCMAKE_TOOLCHAIN_FILE=/path/to/polly/gcc.cmake

Instead of

.. code-block:: none

  > polly.py --toolchain gcc

Get sources:

.. code-block:: none

  > git clone https://github.com/forexample/urho3d-with-hunter
  > cd urho3d-with-hunter
  [urho3d-with-hunter]>

Linux
-----

.. code-block:: none

  [urho3d-with-hunter]> polly.py --toolchain gcc --verbose --config Release

Launch example using CTest:

.. code-block:: none

  [urho3d-with-hunter]> polly.py --toolchain gcc --verbose --config Release --test

Windows
-------

.. code-block:: none

  [urho3d-with-hunter]> polly.py --toolchain vs-14-2015 --verbose --config Release

Launch example using CTest:

.. code-block:: none

  [urho3d-with-hunter]> polly.py --toolchain vs-14-2015 --verbose --config Release --test

OSX
---

.. code-block:: none

  [urho3d-with-hunter]> polly.py --toolchain osx-10-12 --verbose --config Release

Launch example using CTest:

.. code-block:: none

  [urho3d-with-hunter]> polly.py --toolchain osx-10-12 --verbose --config Release --test

Android
-------

.. code-block:: none

  [urho3d-with-hunter]> polly.py --toolchain android-ndk-r15c-api-21-armeabi-v7a-neon-clang-libcxx --verbose --config Release

To build APK and launch it on device add ``--target SkeletalAnimation-launch``:

.. code-block:: none

  [urho3d-with-hunter]> polly.py --toolchain android-ndk-r15c-api-21-armeabi-v7a-neon-clang-libcxx --verbose --config Release --target SkeletalAnimation-launch

iOS
---

.. code-block:: none

  [urho3d-with-hunter]> polly.py --toolchain ios-10-3 --verbose --config Release

To run example add ``--open`` to open Xcode:

.. code-block:: none

  [urho3d-with-hunter]> polly.py --toolchain ios-10-3 --verbose --config Release --open

Select ``SkeletalAnimation`` executable in opened Xcode project and run it.

Screen
------

.. image:: https://user-images.githubusercontent.com/4346993/33789459-90f9ee6e-dc89-11e7-99f4-31ad20f3b1a0.gif

Hunter
------

* https://docs.hunter.sh/en/latest/packages/pkg/Urho3D.html
