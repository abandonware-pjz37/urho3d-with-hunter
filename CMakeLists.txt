cmake_minimum_required(VERSION 3.9)

include("cmake/HunterGate.cmake")
HunterGate(
    URL "https://github.com/ruslo/hunter/archive/v0.19.219.tar.gz"
    SHA1 "a6ed16e70b1c235fdcfef07ad406aa7c737d4be2"
    LOCAL
)

project(Urho3D-example)

hunter_add_package(Urho3D)
find_package(Urho3D CONFIG REQUIRED)

set(
    sources
    Mover.cpp
    Mover.h
    Sample.h
    Sample.inl
    SkeletalAnimation.cpp
    SkeletalAnimation.h
)

if(ANDROID)
  list(APPEND sources "${URHO3D_ROOT}/include/SDL2/android/SDL_android_main.c")
  # On Android we are building '*.so' library that will be loaded from Java code
  add_library(SkeletalAnimation SHARED ${sources})
else()
  add_executable(SkeletalAnimation WIN32 ${sources})
endif()

target_link_libraries(SkeletalAnimation PUBLIC Urho3D::Urho3D)

if(WIN32)
  set(resources "${URHO3D_ROOT}/share/Resources")
else()
  set(resources "${URHO3D_ROOT}/share/Urho3D/Resources")
endif()

if(ANDROID)
  hunter_add_package(Android-Apk)
  list(APPEND CMAKE_MODULE_PATH "${ANDROID-APK_ROOT}")
  include(AndroidApk)

  hunter_add_package(Android-SDK)
  message("Path to `android`: ${ANDROID-SDK_ROOT}/android-sdk/tools/android")
  message("Path to `emulator`: ${ANDROID-SDK_ROOT}/android-sdk/tools/emulator")
  message("Path to `adb`: ${ANDROID-SDK_ROOT}/android-sdk/platform-tools/adb")

  set(apk_directory "${CMAKE_CURRENT_BINARY_DIR}/apk")

  # TODO: Optimal management of resources
  file(REMOVE_RECURSE "${apk_directory}/res")
  file(REMOVE_RECURSE "${apk_directory}/src")

  file(COPY "${CMAKE_CURRENT_LIST_DIR}/android/res" DESTINATION "${apk_directory}")
  file(COPY "${CMAKE_CURRENT_LIST_DIR}/android/src" DESTINATION "${apk_directory}")

  set(local_assets "${CMAKE_CURRENT_BINARY_DIR}/assets")
  file(REMOVE_RECURSE "${local_assets}")
  file(MAKE_DIRECTORY "${local_assets}")

  file(COPY "${resources}/CoreData" DESTINATION "${local_assets}")
  file(COPY "${resources}/Data" DESTINATION "${local_assets}")

  android_create_apk(
      BASE_TARGET SkeletalAnimation
      APK_TARGET SkeletalAnimation-apk
      LAUNCH_TARGET SkeletalAnimation-launch
      PACKAGE_NAME "com.github.urho3d"
      DIRECTORY "${apk_directory}"
      DATA_DIRECTORY "."
      ASSETS "${local_assets}/*"
      MANIFEST_TEMPLATE "${CMAKE_CURRENT_LIST_DIR}/android/AndroidManifest.xml.in"
      ACTIVITY_LAUNCH "SampleLauncher"
  )
else()
  enable_testing()
  add_test(NAME SkeletalAnimation COMMAND SkeletalAnimation -pp "${resources}")
endif()
