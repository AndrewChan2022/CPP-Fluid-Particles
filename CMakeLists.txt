cmake_minimum_required(VERSION 3.8.0 FATAL_ERROR)

if(NOT "${CMAKE_GENERATOR}" MATCHES "(Win64|IA64)")
    message("Please use 64-bit cmake generator.")
endif()

project(CPP_Fluid_Particles VERSION 0.1.0 LANGUAGES CXX C CUDA)

if(${CMAKE_VERSION} VERSION_LESS "3.17.0")
    find_package(CUDA REQUIRED)
    set(CMAKE_CUDA_ARCH 5 6)
else()
    find_package ( CUDAToolkit )
    if ( CUDAToolkit_FOUND )
        enable_language( CUDA )
        set ( CMAKE_CUDA_STANDARD 17 )  # language 11/14/17/20
        set ( CMAKE_CUDA_ARCHITECTURES "60;72;75" ) # 
    endif ()
endif()
# set(CMAKE_CONFIGURATION_TYPES "Release")

set(CUDASAMPLESROOT $ENV{NVCUDASAMPLES_ROOT})
message("cuda samples root ${CUDASAMPLESROOT}")
include_directories(${CUDASAMPLESROOT}/common)
link_directories(${CUDASAMPLESROOT}/common/lib/x64/)

add_subdirectory(src)
