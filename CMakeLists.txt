cmake_minimum_required(VERSION 3.5 FATAL_ERROR)

PROJECT(CAENdrivers)

option(V1718 "Compile and install CAEN V1718 Driver" ON)
option(A2818 "Compile and install CAEN A2818 Driver" ON)
option(A3818 "Compile and install CAEN A3818 Driver" ON)

if(V1718)
    add_subdirectory(V1718)
endif()

if(A2818)
    add_subdirectory(A2818)
endif()

if(A3818)
    add_subdirectory(A3818)
endif()
