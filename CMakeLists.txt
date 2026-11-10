cmake_minimum_required(VERSION 3.20)

project(OptionPricer
    VERSION 0.1.0
    DESCRIPTION "European/American option pricer: Black-Scholes, binomial tree, Monte Carlo"
    LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

if(NOT CMAKE_BUILD_TYPE AND NOT CMAKE_CONFIGURATION_TYPES)
    set(CMAKE_BUILD_TYPE Debug CACHE STRING "Build type" FORCE)
endif()

add_library(pricer_warnings INTERFACE)
if(MSVC)
    target_compile_options(pricer_warnings INTERFACE /W4 /permissive-)
else()
    target_compile_options(pricer_warnings INTERFACE
        -Wall -Wextra -Wpedantic -Wshadow -Wconversion)
endif()

option(PRICER_BUILD_TESTS "Build the unit tests" ON)
if(PRICER_BUILD_TESTS)
    enable_testing()
    add_subdirectory(tests)
endif()
