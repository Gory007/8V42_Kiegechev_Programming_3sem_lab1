cmake_minimum_required(VERSION 3.10.0)
project(lab1 VERSION 0.1.0 LANGUAGES C CXX)

set_property(DIRECTORY . PROPERTY CMAKE_CONFIGURE_DEPENDS main.cpp)

find_package(Git QUIET)

if(GIT_FOUND)
    execute_process(
        COMMAND ${GIT_EXECUTABLE} rev-list --all --count

        WORKING_DIRECTORY ${CMAKE_SOURCE_DIR}
        OUTPUT_VARIABLE GIT_COMMIT_COUNT
        OUTPUT_STRIP_TRAILING_WHITESPACE
    )

else()
    set(GIT_COMMIT_COUNT "0")
endif()

add_definitions(-DVERSION_PROJECT=${GIT_COMMIT_COUNT})

configure_file(version.h.in version.h)

add_executable(lab1 main.cpp)

target_include_directories(lab1 PRIVATE ${CMAKE_CURRENT_BINARY_DIR})

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