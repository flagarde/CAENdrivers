########################################################
# Top-level CMakeLists.txt to build Sauron
cmake_minimum_required(VERSION 3.1)
########################################################

project(V1718)
add_executable(V1718 ${CMAKE_SOURCE_DIR}/cmake/empty.cpp)
add_custom_command(TARGET V1718 PRE_BUILD
                  COMMAND "sudo" "make" "--directory=${CMAKE_SOURCE_DIR}/V1718/linux/CAENUSBdrvB-1.5.2/" 
                  COMMAND "sudo" "make" "--directory=${CMAKE_SOURCE_DIR}/V1718/linux/CAENUSBdrvB-1.5.2/" "install" 
                  COMMAND "sudo" "make" "--directory=${CMAKE_SOURCE_DIR}/V1718/linux/CAENUSBdrvB-1.5.2/" "clean" 
                   )
                   
install(TARGETS V1718 DESTINATION  ${CMAKE_BINARY_DIR} OPTIONAL )
