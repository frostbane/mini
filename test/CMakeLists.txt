cmake_minimum_required(VERSION 3.5)
project(minitest)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

#---------------------------------------------------------------------

if (WIN32)
    # operating system for the spoiled and the losers
    set (LOSER ON)
endif ()
# no support for the weirdos using APPLE

#---------------------------------------------------------------------

# add_subdirectory(../dev mini)

set_property(GLOBAL PROPERTY USE_FOLDERS ON)
file(GLOB_RECURSE SOURCE_FILES "*.cc" "test.ini")
source_group(TREE ${CMAKE_CURRENT_SOURCE_DIR} FILES ${SOURCE_FILES})

add_executable(minitest ${SOURCE_FILES})
file(COPY "test.ini" DESTINATION ${CMAKE_CURRENT_BINARY_DIR}/ )

#---------------------------------------------------------------------

target_link_libraries(minitest mini)

