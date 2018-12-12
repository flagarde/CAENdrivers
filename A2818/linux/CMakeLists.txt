########################################################
# Top-level CMakeLists.txt to build Sauron
cmake_minimum_required(VERSION 3.1)
########################################################

project(A2818)
set(DIR "${CMAKE_SOURCE_DIR}/A2818/linux/A2818Drv-1.20")


execute_process(COMMAND ls /dev/a2818_* OUTPUT_VARIABLE A2818_DETECTED OUTPUT_STRIP_TRAILING_WHITESPACE OUTPUT_QUIET ERROR_QUIET)
if ("${A2818_DETECTED}" STREQUAL "")
 message("-- A2818 not detected ! Abording compilation")
 add_custom_target(A2818 COMMAND "")
else()
    message("-- A2818 devices detected")
    string(SUBSTRING ${CMAKE_HOST_SYSTEM_VERSION} 0 4 LINUX_VERSION)
    string(COMPARE GREATER ${LINUX_VERSION} "2.5" LINUX_VERSION)
    if( ${LINUX_VERSION}  STREQUAL "0" )
    message("-- Linux version inferior to 2.6")
    set(CAEN_DRIVERS_MAKEFILE ${DIR}/Makefile.2.4)
    set(CAEN_DRIVERS_SCRIPT ${DIR}/a2818_load.2.4)
    else()
    message("-- Linux version superior to 2.6")
    set(CAEN_DRIVERS_MAKEFILE ${DIR}/Makefile.2.6-3.x)
    set(CAEN_DRIVERS_SCRIPT ${DIR}/a2818_load.2.6-3.x)
    endif()
    message("-- ${CAEN_DRIVERS_MAKEFILE}")
    message("-- ${CAEN_DRIVERS_SCRIPT}")
    add_custom_target(A2818
                  COMMAND "sudo" "make" "--makefile=${CAEN_DRIVERS_MAKEFILE}" "--directory=${DIR}" 
                  COMMAND "sudo" "sh" "${CAEN_DRIVERS_SCRIPT}"
                  COMMAND "sudo" "make" "--makefile=${CAEN_DRIVERS_MAKEFILE}" "--directory=${DIR}" "clean"
              WORKING_DIRECTORY "${CMAKE_SOURCE_DIR}/build"
                  )
endif()
