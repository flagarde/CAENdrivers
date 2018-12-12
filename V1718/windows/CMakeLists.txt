########################################################
# Top-level CMakeLists.txt to build Sauron
cmake_minimum_required(VERSION 3.1)
########################################################

project(V1718)

if(${BITS}  STREQUAL "64")
    ## Check for Version ##
    if( ${CMAKE_SYSTEM_VERSION} EQUAL 6.1 ) # Windows 7
        set(DIR "${CMAKE_SOURCE_DIR}/V1718/windows/x64/V1718Drv-7x64/CAENV1718drv.inf")
    elseif( ${CMAKE_SYSTEM_VERSION} EQUAL 6.2 ) # Windows 8
        set(DIR "${CMAKE_SOURCE_DIR}/V1718/windows/x64/V1718Drv-8-8.1x64/CAENUSBdrv.inf")
    else() # Some other Windows
        set(DIR "${CMAKE_SOURCE_DIR}/V1718/windows/x64/CAENUSBDrv-win10_x64-1.2.3.20/caenusbdrv.inf")
    endif()
else()
    set(DIR "${CMAKE_SOURCE_DIR}/V1718/windows/x86/CAENV1718drv.inf")
endif()


add_custom_target(V1718 
                  COMMAND "pnputil -i -a ${DIR}" 
                  WORKING_DIRECTORY "${CMAKE_SOURCE_DIR}/build"
                 )
