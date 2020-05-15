cmake_minimum_required(VERSION 3.13)
project(thpool_project C)

# THIS FILE IS JUST FOR COMPILATION!
# IT IS MEANT TO BE INCLUDED AS PART OF YOUR CMAKE SOURCE TREE!

# Disable any debug printing in release
set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -DDISABLE_PRINT")

# Add TinyCThread from parent (will be changed, ideally merged with said library)
# TinyCThread (emulation of C11 threading API, used as we are missing C11 threading API on Windows completely)
option(TINYCTHREAD_DISABLE_TESTS "Disable TinyCThread unit tests" ON)
option(TINYCTHREAD_INSTALL "Install a static library for TinyCThread" OFF)
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../tinycthread ${CMAKE_CURRENT_BINARY_DIR}/tinycthread)

add_library(thpool STATIC thpool/thpool.c)
target_include_directories(thpool PUBLIC thpool)
target_link_libraries(thpool PUBLIC tinycthread)
