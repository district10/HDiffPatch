cmake_minimum_required(VERSION 3.5)
project(HDiffPatchPackage)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(CMAKE_POSITION_INDEPENDENT_CODE ON)

if(NOT CMAKE_BUILD_TYPE OR CMAKE_BUILD_TYPE STREQUAL "")
    set(CMAKE_BUILD_TYPE "Release" CACHE STRING "" FORCE)
    message(STATUS "Set build type to default: ${CMAKE_BUILD_TYPE}")
else()
    message(STATUS "Your build type: ${CMAKE_BUILD_TYPE}")
endif()
if(CMAKE_BUILD_TYPE STREQUAL "Debug")
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -O0 -ggdb")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O0 -ggdb")
elseif(CMAKE_BUILD_TYPE STREQUAL "Release")
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -O3")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O3")
endif()

macro(print_include_directories)
    get_property(
        dirs
        DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
        PROPERTY INCLUDE_DIRECTORIES)
    message(STATUS "all include directories:")
    foreach(dir ${dirs})
        message(STATUS "-   ${dir}")
    endforeach()
endmacro()

macro(print_all_linked_libraries target)
    get_target_property(libs ${target} LINK_LIBRARIES)
    message(STATUS "all linked libraries: (against ${target})")
    foreach(lib ${libs})
        message(STATUS "-   ${lib}")
    endforeach()
endmacro()

macro(print_all_variables)
    get_cmake_property(vars VARIABLES)
    list(SORT vars)
    message(STATUS "all variables:")
    foreach(var ${vars})
        message(STATUS "-   ${var}=${${var}}")
    endforeach()
endmacro()

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/bin)

include_directories(BEFORE ${CMAKE_CURRENT_LIST_DIR})

add_subdirectory(libHDiffPatch)
add_subdirectory(dirDiffPatch)
add_subdirectory(bsdiff_wrapper)
add_subdirectory(vcdiff_wrapper)

set(CMAKE_CXX_STANDARD 11)

# include_directories(BEFORE ${CUBAO_INCLUDE})
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Werror")
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -Werror")

set(SOURCES
    compress_parallel.cpp
    file_for_patch.c
)
add_library(${PROJECT_NAME} ${SOURCES})

set(LIBS
    ${PROJECT_NAME}
    HDiffPatch
    bsdiff_wrapper
    dirDiffPatch
    vcdiff_wrapper
)

# add_executable(hpatchz hpatchz.c)
# target_link_libraries(hpatchz ${LIBS})

# add_executable(hdiffz hdiffz.cpp)
# target_link_libraries(hdiffz ${LIBS})

option(BUILD_TESTS "Build tests." ON)
if(BUILD_TESTS)
    add_subdirectory(test)
endif()