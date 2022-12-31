cmake_minimum_required(VERSION 3.5)
project(lzma)

set(CMAKE_CXX_STANDARD 11)
file(GLOB HEADERS *.h)
file(GLOB SOURCES *.c)
add_library(${PROJECT_NAME} ${SOURCES} ${HEADERS})
