cmake_minimum_required(VERSION 3.5)

project(LAZPERF VERSION 2.1.0)

set(ROOT_DIR ${PROJECT_SOURCE_DIR})
include(${ROOT_DIR}/cmake/common.cmake NO_POLICY_SCOPE)

# Allow advanced users to generate Makefiles printing detailed commands
mark_as_advanced(CMAKE_VERBOSE_MAKEFILE)

# Path to additional CMake modules
set(CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake/modules ${CMAKE_MODULE_PATH})

#------------------------------------------------------------------------------
# general settings
#------------------------------------------------------------------------------

# Choose package components
set(WITH_TESTS TRUE CACHE BOOL "Choose if LAZPERF unit tests should be built")

if (EMSCRIPTEN)
    set(WITH_TESTS NO)
else()
    include(${LAZPERF_CMAKE_DIR}/install.cmake)
endif()

if(WITH_TESTS)
    enable_testing()
    file (DOWNLOAD
        "https://github.com/PDAL/data/raw/master/autzen/autzen.laz"
        "cpp/test/raw-sets/autzen.laz")
endif()

add_subdirectory(cpp)
