cmake_minimum_required(VERSION 3.10)
project(minitest)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

#---------------------------------------------------------------------

option(NDEBUG "Build in release mode and disable asserts." ON)

#---------------------------------------------------------------------

if (WIN32)
    # operating system for the spoiled and the losers
    set (LOSER ON)
endif ()

if (APPLE)
    # no support for the weirdos using APPLE
    set (BANANA ON)
endif()

if (VERBOSE)
    set (CMAKE_VERBOSE_MAKEFILE ON)
endif ()

#---------------------------------------------------------------------

set_property(GLOBAL PROPERTY USE_FOLDERS ON)
file(GLOB_RECURSE SOURCE_FILES "*.cc" "test.ini")
source_group(TREE ${CMAKE_CURRENT_SOURCE_DIR} FILES ${SOURCE_FILES})

add_executable(minitest ${SOURCE_FILES})
file(COPY "test.ini" DESTINATION ${CMAKE_CURRENT_BINARY_DIR}/ )

#---------------------------------------------------------------------

if (NDEBUG)
    # release
    set (CMAKE_BUILD_TYPE "Release")
    add_definitions (-DNDEBUG)
else ()
    # debug
    set (CMAKE_BUILD_TYPE "Debug")
    # remove_definitions (-DNDEBUG)
endif ()

#---------------------------------------------------------------------

target_link_libraries(minitest mini)

