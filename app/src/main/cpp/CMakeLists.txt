
cmake_minimum_required(VERSION 3.22.1)


project("vulkanndk")

set(APP_GLUE_DIR D:/Android/android-sdk/ndk/25.1.8937393/sources/android/native_app_glue)

add_library(native_app STATIC ${APP_GLUE_DIR}/android_native_app_glue.c)

target_include_directories(native_app PUBLIC
        ${ANDROID_NDK}/sources/android/native_app_glue)

add_library(${CMAKE_PROJECT_NAME} SHARED
        # List C/C++ source files with relative paths to this CMakeLists.txt.
        VulkanMain.cpp)

set(CMAKE_SHARED_LINKER_FLAGS "${CMAKE_SHARED_LINKER_FLAGS} -u ANativeActivity_onCreate")

target_link_libraries(${CMAKE_PROJECT_NAME}
        # List libraries link to the target library
        android
        native_app
        log)