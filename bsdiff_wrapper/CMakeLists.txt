cmake_minimum_required(VERSION 3.5)
project(bsdiff_wrapper)

set(CMAKE_CXX_STANDARD 11)
set(HEADERS bsdiff_wrapper.h bspatch_wrapper.h)
set(SOURCES bsdiff_wrapper.cpp bspatch_wrapper.c)
add_library(${PROJECT_NAME} ${SOURCES} ${HEADERS})