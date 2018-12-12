########################################################
# Top-level CMakeLists.txt to build Sauron
cmake_minimum_required(VERSION 3.1)
########################################################

project(A3818)
set(DIR "${CMAKE_SOURCE_DIR}/A3818/linux/A3818Drv-1.6.1")


execute_process(COMMAND ls /dev/a3818_* OUTPUT_VARIABLE A3818_DETECTED OUTPUT_STRIP_TRAILING_WHITESPACE OUTPUT_QUIET ERROR_QUIET)
if ("${A2818_DETECTED}" STREQUAL "")
 message("-- A3818 not detected ! Abording compilation")
 add_custom_target(A3818 COMMAND "")
else()
    message("-- A3818 devices detected")
    add_custom_target(A3818
                  COMMAND "sudo" "make" "--makefile=${CAEN_DRIVERS_MAKEFILE}" "--directory=${DIR}" 
                  COMMAND "sudo" "make" "--makefile=${CAEN_DRIVERS_MAKEFILE}" "--directory=${DIR}" "install"
                  COMMAND "sudo" "make" "--makefile=${CAEN_DRIVERS_MAKEFILE}" "--directory=${DIR}" "clean"
              WORKING_DIRECTORY "${CMAKE_SOURCE_DIR}/build"
                  )
endif()
