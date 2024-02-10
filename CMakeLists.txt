cmake_minimum_required(VERSION 3.27)

project(cpp_template)

set(CMAKE_CXX_STANDARD 20)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

option(USE_UBSAN "Enable Undefined Behavior Sanitizer" OFF)
option(USE_ASAN "Enable Address Sanitizer" OFF)
option(USE_TSAN "Enable Thread Sanitizer" OFF)
option(USE_LIBFUZZER "Enable LibFuzzer" OFF)

if (USE_UBSAN)
    add_compile_options(
        "-fsanitize=undefined"
        "-fno-omit-frame-pointer")
    add_link_options("-fsanitize=undefined")
endif()

if (USE_ASAN)
    add_compile_options(
        "-fsanitize=address"
        "-fno-omit-frame-pointer")
    add_link_options("-fsanitize=address")
endif()

if (USE_TSAN)
    add_compile_options(
        "-fsanitize=thread"
        "-fno-omit-frame-pointer")
    add_link_options("-fsanitize=thread")
endif()

if (USE_LIBFUZZER)
    add_compile_options("-fsanitize=fuzzer")
    add_link_options("-fsanitize=fuzzer")
endif()

include(cmake/gtest.cmake)
include(cmake/helpers.cmake)

add_subdirectory(3party/fmt)

add_subdirectory(lib)
add_subdirectory(cmd)
add_subdirectory(test)