cmake_minimum_required(VERSION 3.1)
project(libuvc VERSION 0.0.6 LANGUAGES C)

set(libuvc_VERSION_MAJOR 0)
set(libuvc_VERSION_MINOR 0)
set(libuvc_VERSION_PATCH 6)
set(libuvc_VERSION ${libuvc_VERSION_MAJOR}.${libuvc_VERSION_MINOR}.${libuvc_VERSION_PATCH})

set(SOURCES
        libuvc/src/ctrl.c
        libuvc/src/ctrl-gen.c
        libuvc/src/device.c
        libuvc/src/diag.c
        libuvc/src/frame.c
        libuvc/src/init.c
        libuvc/src/stream.c
        libuvc/src/misc.c
        libuvc/src/frame-mjpeg.c
        )

find_package(libusb REQUIRED CONFIG)
find_package(libjpeg-turbo REQUIRED CONFIG)

add_library(uvc SHARED ${SOURCES})

target_include_directories(uvc PRIVATE ./include ./libuvc/include)

target_link_libraries(uvc PRIVATE libjpeg-turbo::jpeg libusb::usb1.0)
