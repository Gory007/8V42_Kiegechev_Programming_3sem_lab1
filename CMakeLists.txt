cmake_minimum_required(VERSION 3.10.0)
project(lab1 VERSION 0.1.0 LANGUAGES C CXX)

add_executable(lab1 main.cpp)

if(DEFINED PROJECT_VERSION)
    message(STATUS "Project version: ${PROJECT_VERSION}")
    target_compile_definitions(lab1 PRIVATE PROJECT_VERSION="${PROJECT_VERSION}")
endif()