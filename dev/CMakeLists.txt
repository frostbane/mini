cmake_minimum_required(VERSION 3.10)
project(mini)

#---------------------------------------------------------------------

option(NDEBUG "Build in release mode and disable asserts." ON)
option(INI_UNICODE "Build with unicode support provided by the operating system." ON)
option(INI_ANSIONLY "Ignore unicode support provided by the compiler. This overrides the UNICODE option." OFF)
option(INI_GLUE "INI glue file header to use." OFF)
option(INI_BUFFERSIZE "Maximum line length supported and maximum file path for temporary files." OFF) # 512
option(INI_LINETERM "Line terminator. Default: CRLF" OFF) # "\r\n"
option(INI_READONLY "Disable writing into INI files." OFF)
option(INI_REAL "Add support for rational numbers" OFF)
option(INI_NOBROWSE "Disable the ini_browse function." OFF)
option(PORTABLE_STRNICMP "Use a portable implementation of strnicpm" OFF)
option (VERBOSE "Verbose console output." OFF)

#---------------------------------------------------------------------

if (${CMAKE_SYSTEM_NAME} MATCHES "Linux")
    set (LINUX ON)
endif()

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
file(GLOB_RECURSE SOURCE_FILES "*.c" "*.h")

if (LOSER)
    file(GLOB_RECURSE HEADER_FILES "*.h")
    source_group(TREE "${CMAKE_CURRENT_SOURCE_DIR}" FILES ${HEADER_FILES})
else ()
    set (HEADER_FILES "")
endif ()

include_directories(${CMAKE_CURRENT_SOURCE_DIR})
add_library(mini ${SOURCE_FILES} ${HEADER_FILES})
target_include_directories(mini PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

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

if (INI_GLUE)
    add_definitions ("-DINI_GLUE_${INI_GLUE}")
endif ()

if (INI_UNICODE AND NOT LINUX)
    add_definitions (-DUNICODE)
endif ()

if (INI_ANSIONLY OR LINUX)
    add_definitions (-DINI_ANSIONLY)
endif ()

if (INI_BUFFERSIZE)
    add_definitions ("-DINI_BUFFERSIZE=${INI_BUFFERSIZE}")
endif ()

if (INI_LINETERM)
    add_definitions ("-DINI_LINETERM=${INI_LINETERM}")
endif ()

if (INI_READONLY)
    add_definitions (-DINI_READONLY)
endif ()

if (INI_REAL)
    add_definitions (-DINI_REAL)
endif ()

if (INI_NOBROWSE)
    add_definitions (-DINI_NOBROWSE)
endif ()

if (PORTABLE_STRNICMP)
    add_definitions (-DPORTABLE_STRNICMP)
endif ()

#---------------------------------------------------------------------
