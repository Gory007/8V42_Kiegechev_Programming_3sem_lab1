cmake_minimum_required(VERSION 3.10.0)
project(lab1 VERSION 0.1.0 LANGUAGES C CXX)

if(DEFINED VERSION_PROJECT)
    add_definitions(-DVERSION_PROJECT="${VERSION_PROJECT}")
else()
    add_definitions(-DVERSION_PROJECT="0")
endif()

add_executable(lab1 main.cpp)



set(CPACK_PACKAGE_NAME "lab1")

set(CPACK_PACKAGE_VERSION ${PROJECT_VERSION})

if(WIN32)
    set(CPACK_GENERATOR "ZIP")
endif()

if(UNIX AND NOT APPLE)
    set(CPACK_GENERATOR "DEB")
    set(CPACK_DEBIAN_PACKAGE_MAINTAINER "Kiegechev Pavel <kiegechev09@gmail.com>")
endif()

install(TARGETS lab1 DESTINATION bin)
include(CPack)