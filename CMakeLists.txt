cmake_minimum_required(VERSION 3.16)

option(BUILD_TESTS "Build test programs" OFF)

project(bcrypt)

set(CMAKE_CXX_STANDARD 11)

# Disable -Wformat-truncation
if(CMAKE_CXX_COMPILER_ID STREQUAL "GNU")
  add_compile_options(-Wno-format-truncation)
endif()

add_library(bcrypt src/bcrypt.cpp src/blowfish.cpp)
target_include_directories(bcrypt PRIVATE src/)
target_include_directories(bcrypt PUBLIC include/)

if(BUILD_TESTS)
  add_executable(test test/main.cpp)
  target_link_libraries(test PRIVATE bcrypt)
endif()
