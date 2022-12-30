cmake_minimum_required(VERSION 3.5)
project(md5)

set(CMAKE_CXX_STANDARD 11)
add_library(md5 md5.c md5.h)
add_executable(md5main md5main.c)
target_link_libraries(md5main md5)
