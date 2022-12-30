cmake_minimum_required(VERSION 3.5)
project(HDiffPatch)

set(CMAKE_CXX_STANDARD 11)
file(GLOB_RECURSE HEADERS **/*.h)
file(GLOB_RECURSE SOURCES **/*.c **/*.cpp)
add_library(${PROJECT_NAME} ${SOURCES} ${HEADERS})
