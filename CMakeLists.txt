# YOU PROBABLY DON'T HAVE TO USE THIS CMAKE PROJECT, IT'S JUST A SINGLE
#  C FILE. COPY IT INTO YOUR PROJECT INSTEAD.

cmake_minimum_required(VERSION 3.12.0)
project(mojoAL LANGUAGES C)

find_package(SDL3 REQUIRED CONFIG REQUIRED COMPONENTS SDL3)

add_library(mojoal SHARED mojoal.c)
target_include_directories(mojoal PRIVATE AL)
target_link_libraries(mojoal PRIVATE SDL3::SDL3)

macro(add_test_executable _NAME)
    add_executable(${_NAME} tests/${_NAME}.c)
    target_link_libraries(${_NAME}
        PUBLIC mojoal
        PRIVATE SDL3::SDL3)
endmacro()

add_test_executable(testopenalinfo)
add_test_executable(testqueueing)
add_test_executable(testcapture)
add_test_executable(testposition)
