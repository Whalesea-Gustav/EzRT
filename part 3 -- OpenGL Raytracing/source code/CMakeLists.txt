# cmake version
cmake_minimum_required(VERSION 3.1)

# c++11
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# vcpkg
if(DEFINED ENV{VCPKG_ROOT} AND NOT DEFINED CMAKE_TOOLCHAIN_FILE)
	set(CMAKE_TOOLCHAIN_FILE "$ENV{VCPKG_ROOT}/scripts/buildsystems/vcpkg.cmake" CACHE STRING "")
endif()
if(DEFINED ENV{VCPKG_DEFAULT_TRIPLET} AND NOT DEFINED VCPKG_TARGET_TRIPLET)
	set(VCPKG_TARGET_TRIPLET "$ENV{VCPKG_DEFAULT_TRIPLET}" CACHE STRING "")
endif()

set(TARGET_NAME "OpenGLRayTracing")

# project
project(${TARGET_NAME})

# target
aux_source_directory("./lib" CPP_FILES)
add_executable(${TARGET_NAME} main.cpp ${CPP_FILES})
target_include_directories(${TARGET_NAME} PRIVATE include)

# dependency
find_package(GLEW REQUIRED)
find_package(GLUT REQUIRED)
find_package(GLM REQUIRED)

# link
target_link_libraries(${TARGET_NAME} PRIVATE GLUT::GLUT)
target_link_libraries(${TARGET_NAME} PRIVATE GLEW::GLEW)
