cmake_minimum_required(VERSION 2.8)
project(ibmP)

find_package(MPI REQUIRED)
add_definitions(-DOMPI_SKIP_MPICXX)
include_directories(${MPI_INCLUDE_PATH})

OPTION (USE_OpenMP "Use OpenMP" ON)
IF(USE_OpenMP)
  FIND_PACKAGE(OpenMP REQUIRED)
  IF(OPENMP_FOUND)
    SET(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${OpenMP_C_FLAGS}")
    SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
  ENDIF()
ENDIF()

# Set your fftw3 path here. Only works with cmake install of fftw3
#SET(FFTW3_DIR "/home/anthony/fftw-3.3.8")
#find_package(FFTW3 REQUIRED)

add_subdirectory(solver)
include_directories(solver)
add_subdirectory(boundary)
include_directories(boundary)
add_subdirectory(exe)

file(COPY input DESTINATION ${CMAKE_CURRENT_BINARY_DIR}/exe)

