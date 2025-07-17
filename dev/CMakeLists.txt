cmake_minimum_required(VERSION 3.5)
project(mini)

if (WIN32)
    # operating system for the spoiled and the losers
    set (LOSER ON)
endif ()

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

