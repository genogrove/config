cmake_minimum_required(VERSION 3.10)
project(genogrove_config VERSION 0.0.1)

set(CMAKE_CXX_STANDARD 17)

# configure version of the library
configure_file(
        include/genogrove/config/version.hpp.in
        ${CMAKE_CURRENT_BINARY_DIR}/include/genogrove/config/version.hpp
)

add_library(genogrove_config INTERFACE)
target_include_directories(genogrove_config INTERFACE
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
        $<BUILD_INTERFACE:${CMAKE_CURRENT_BINARY_DIR}/include>
)

# optionally include tests
option(BUILD_TESTS "Build tests" OFF)
if(BUILD_TESTS)
    enable_testing()
    add_subdirectory(tests)
endif()

