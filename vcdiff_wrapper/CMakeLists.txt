cmake_minimum_required(VERSION 3.5)
project(vcdiff_wrapper)

set(CMAKE_CXX_STANDARD 11)
file(GLOB HEADERS *.h)
file(GLOB SOURCES *.c *.cpp)
add_library(${PROJECT_NAME} ${SOURCES} ${HEADERS})
