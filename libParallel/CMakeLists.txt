cmake_minimum_required(VERSION 3.5)
project(Parallel)

set(CMAKE_CXX_STANDARD 11)
file(GLOB HEADERS *.h)
file(GLOB SOURCES *.cpp)
add_library(${PROJECT_NAME} ${SOURCES} ${HEADERS})
