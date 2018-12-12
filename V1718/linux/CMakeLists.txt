########################################################
# Top-level CMakeLists.txt to build Sauron
cmake_minimum_required(VERSION 3.1)
########################################################

project(V1718)

add_custom_target(V1718 
                  COMMAND "sudo" "make" "--directory=${CMAKE_SOURCE_DIR}/V1718/linux/CAENUSBdrvB-1.5.2/" 
                  COMMAND "sudo" "make" "--directory=${CMAKE_SOURCE_DIR}/V1718/linux/CAENUSBdrvB-1.5.2/" "install" 
                  COMMAND "sudo" "make" "--directory=${CMAKE_SOURCE_DIR}/V1718/linux/CAENUSBdrvB-1.5.2/" "clean" 
                  WORKING_DIRECTORY "${CMAKE_SOURCE_DIR}/build"
                 )
