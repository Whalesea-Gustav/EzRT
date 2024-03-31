cmake_minimum_required(VERSION 3.22)
project(EzRT)

# c++11
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# vcpkg
if(DEFINED ENV{VCPKG_ROOT} AND NOT DEFINED CMAKE_TOOLCHAIN_FILE)
    set(CMAKE_TOOLCHAIN_FILE "$ENV{VCPKG_ROOT}/scripts/buildsystems/vcpkg.cmake" CACHE STRING "")
endif()
if(DEFINED ENV{VCPKG_DEFAULT_TRIPLET} AND NOT DEFINED VCPKG_TARGET_TRIPLET)
    set(VCPKG_TARGET_TRIPLET "$ENV{VCPKG_DEFAULT_TRIPLET}" CACHE STRING "")
endif()

if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE "Release" CACHE STRING "Choose the type of build, options are: Debug Release RelWithDebInfo MinSizeRel." FORCE)
endif()

if(CMAKE_BUILD_TYPE STREQUAL "Debug")
    set(EXECUTABLE_OUTPUT_PATH  "${PROJECT_BINARY_DIR}/../bin/debug")
else()
    set(EXECUTABLE_OUTPUT_PATH  "${PROJECT_BINARY_DIR}/../bin/release")
endif()

# dependency
find_package(GLEW REQUIRED)
find_package(GLUT REQUIRED)
find_package(GLM CONFIG REQUIRED)
find_package(OpenMP)

include_directories(include)

add_subdirectory("part 1 -- Basic Raytracing with C++")
add_subdirectory("part 2 -- BVH Accelerate Struct")
add_subdirectory("part 3 -- OpenGL Raytracing")
add_subdirectory("part 4 -- Disney Principle BRDF")


