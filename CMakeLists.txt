cmake_minimum_required(VERSION 3.9)
project(hello_world)

# Macro: list sub directories
# Ref: https://stackoverflow.com/questions/7787823/cmake-how-to-get-the-name-of-all-subdirectories-of-a-directory
macro(SUBDIRLIST result curdir includedir)
    file(GLOB children RELATIVE ${curdir} ${curdir}/*)
    set(dirlist "")
    foreach(child ${children})
        if(IS_DIRECTORY ${curdir}/${child})
            # message(WARNING ${curdir}/${child}/${includedir}) # for CLion debugging only
            LIST(APPEND dirlist ${curdir}/${child}/${includedir})
        endif()
    endforeach()
    set(${result} ${dirlist})
endmacro()

# Project info
set(CMAKE_CXX_STANDARD 11)
set(IDF_PATH "$ENV{IDF_PATH}")
set(CMAKE_SYSTEM_NAME xtensa-esp32-elf)
set(CMAKE_C_COMPILER xtensa-esp32-elf-gcc)
set(CMAKE_FIND_ROOT_PATH "${IDF_PATH}../xtensa-esp32-elf/")

# ESP-IDF related stuff
file(GLOB_RECURSE SOURCES "${IDF_PATH}/*.c")

# Find out all ESP-IDF components and add them to include list
set(INCLUDE_DIRS "")
SUBDIRLIST(INCLUDE_DIRS ${IDF_PATH}/components include/)

list(REMOVE_DUPLICATES INCLUDE_DIRS)
include_directories(${INCLUDE_DIRS})
include_directories("build/include")

#[[# Arduino libraries
set(ARDUINO_LIBS_INCLUDE_DIRS "")
SUBDIRLIST(ARDUINO_LIBS_INCLUDE_DIRS "${CMAKE_CURRENT_SOURCE_DIR}/components/arduino/libraries" src/)
list(REMOVE_DUPLICATES ARDUINO_LIBS_INCLUDE_DIRS)
include_directories(${ARDUINO_LIBS_INCLUDE_DIRS})

# Arduino framework
include_directories("components/arduino/cores/esp32/")]]

# Fake exec
add_executable(hello_world
        main/hello_world_main.c)