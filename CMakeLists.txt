cmake_minimum_required(VERSION 3.8.2)

project(OpenMPL)

set(CMAKE_INSTALL_PREFIX "${CMAKE_CURRENT_SOURCE_DIR}" CACHE PATH "Prefix prepended to install directories")
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_CURRENT_SOURCE_DIR}/cmake")

if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE "Release" CACHE STRING
        "Choose the type of build, options are: Debug Release."
        FORCE)
endif(NOT CMAKE_BUILD_TYPE)
message("-- CMAKE_BUILD_TYPE: ${CMAKE_BUILD_TYPE}")

if(NOT CMAKE_CXX_ABI)
    set(CMAKE_CXX_ABI 0 CACHE STRING
        "Choose the value for _GLIBCXX_USE_CXX11_ABI, options are: 0|1."
        FORCE)
endif(NOT CMAKE_CXX_ABI)
message("-- CMAKE_CXX_ABI: _GLIBCXX_USE_CXX11_ABI=${CMAKE_CXX_ABI}")
add_definitions(-D_GLIBCXX_USE_CXX11_ABI=${CMAKE_CXX_ABI})

#option(ENABLE_GUROBI "whether enable Gurobi" OFF)
#message("-- GUROBI: ${ENABLE_GUROBI}")
#option(ENABLE_LEMONCBC "whether enable Lemon-CBC" OFF)
#message("-- LEMONCBC: ${ENABLE_LEMONCBC}")
#option(ENABLE_CSDP "whether enable CSDP" OFF)
#message("-- CSDP: ${ENABLE_CSDP}")

set(CMAKE_CXX_STANDARD 11)

set(LIMBO_SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/thirdparty/Limbo)
message("-- LIMBO_SOURCE_DIR ${LIMBO_SOURCE_DIR}")
set(LIMBO_BINARY_DIR ${CMAKE_CURRENT_BINARY_DIR}/thirdparty/Limbo)
message("-- LIMBO_BINARY_DIR ${LIMBO_BINARY_DIR}")

find_package(ZLIB REQUIRED)
find_package(Boost 1.55.0 REQUIRED COMPONENTS iostreams chrono timer unit_test_framework graph regex)
find_package(Gurobi)

add_subdirectory(thirdparty)
add_subdirectory(src)
