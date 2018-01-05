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

* https://docs.hunter.sh/en/latest/packages/pkg/Urho3D.html

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
