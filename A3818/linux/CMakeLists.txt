########################################################
# Top-level CMakeLists.txt to build Sauron
cmake_minimum_required(VERSION 3.1)
########################################################

project(A3818)
set(DIR "${CMAKE_SOURCE_DIR}/A3818/linux/A3818Drv-1.6.1")
add_executable(A3818 ${CMAKE_SOURCE_DIR}/cmake/empty.cpp)

execute_process(COMMAND ls /dev/a3818_* OUTPUT_VARIABLE A3818_DETECTED OUTPUT_STRIP_TRAILING_WHITESPACE OUTPUT_QUIET ERROR_QUIET)
if ("${A2818_DETECTED}" STREQUAL "")
 message("-- A3818 not detected ! Abording compilation")
 add_custom_command(TARGET A3818 PRE_BUILD COMMAND "")
else()
    message("-- A3818 devices detected")
    add_custom_command(TARGET A3818 PRE_BUILD
                  COMMAND "sudo" "make" "--makefile=${CAEN_DRIVERS_MAKEFILE}" "--directory=${DIR}" 
                  COMMAND "sudo" "make" "--makefile=${CAEN_DRIVERS_MAKEFILE}" "--directory=${DIR}" "install"
                  COMMAND "sudo" "make" "--makefile=${CAEN_DRIVERS_MAKEFILE}" "--directory=${DIR}" "clean"
                  )
    install(TARGETS A3818 DESTINATION  ${CMAKE_BINARY_DIR} OPTIONAL )
endif()
