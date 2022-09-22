# -------------------------------------------------------------------------------
# Zephyr Griffin Application
#
# Copyright (c) 2022 Trackunit
# SPDX-License-Identifier: Apache-2.0

cmake_minimum_required(VERSION 3.15.0)

project(PROJECT_NAME_HERE LANGUAGES C CXX ASM)


# get app version from git
set(APP_VERSION "0.0.0")
# find_package(Git QUIET)
# if(GIT_FOUND)
#     execute_process(
#         COMMAND ${GIT_EXECUTABLE} describe --always --dirty
#         WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
#         OUTPUT_VARIABLE APP_VERSION
#         OUTPUT_STRIP_TRAILING_WHITESPACE ERROR_STRIP_TRAILING_WHITESPACE
#     )
# endif()
message(STATUS "Application version: " ${APP_VERSION})
configure_file(app_version.h.in ${CMAKE_BINARY_DIR}/app_version.h)
set(CONFIG_KERNEL_BIN_NAME "tu700")
message(STATUS "CONFIG_KERNEL_BIN_NAME: " ${CONFIG_KERNEL_BIN_NAME})
string(APPEND CONFIG_KERNEL_BIN_NAME "_${APP_VERSION}")
message(STATUS "CONFIG_KERNEL_BIN_NAME: " ${CONFIG_KERNEL_BIN_NAME})

find_package(Zephyr REQUIRED HINTS $ENV{ZEPHYR_BASE})

target_include_directories(app PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}/src
)

file(GLOB_RECURSE app_src
    ${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/src/*.c
)

target_sources(app PRIVATE
    ${app_src}
)
