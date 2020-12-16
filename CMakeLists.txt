#mkdir buildPi
#cd buildPi
#cmake -DCMAKE_TOOLCHAIN_FILE=/home/dev/oosman/pi/Toolchain-RaspberryPi.cmake ../
#make VERBOSE=1 -j8

cmake_minimum_required(VERSION 3.12 FATAL_ERROR)

set(PROJ usb)
PROJECT(${PROJ})

set(CMAKE_C_FLAGS "-Wall -pthread")
set(CMAKE_C_FLAGS_DEBUG "-g -O0")
set(CMAKE_C_FLAGS_RELEASE "-O3")
set(CMAKE_CXX_FLAGS "${CMAKE_C_FLAGS} -std=c++14 -lstdc++")
set(CMAKE_CXX_FLAGS_DEBUG ${CMAKE_C_FLAGS_DEBUG})
set(CMAKE_CXX_FLAGS_RELEASE ${CMAKE_C_FLAGS_RELEASE})



FILE(GLOB SRC_FILES
        libusb/*.c
        libusb/os/linux*.c
        libusb/os/events_posix.c
        libusb/os/events_posix.h
        libusb/os/threads_posix.c
        libusb/os/threads_posix.h
    )
add_library(${PROJ} SHARED
    ${SRC_FILES}
  )
target_include_directories(${PROJ} PRIVATE
    .
    ./libusb
	../systemd/src/libudev/
    )

