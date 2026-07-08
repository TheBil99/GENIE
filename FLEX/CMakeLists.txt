cmake_minimum_required(VERSION 3.12...3.30)
project(FLEX LANGUAGES C CXX)


include_directories(include/)

if (POLICY CMP0167)
    cmake_policy(SET CMP0167 OLD)
endif ()
find_package(Boost REQUIRED)
find_package(GSL REQUIRED)
include_directories(${Boost_INCLUDE_DIRS} ${GSL_INCLUDE_DIRS})

set(CMAKE_CXX_FLAGS "-std=c++0x -O3 -lrt -lpthread ")

IF (NOT DEFINED SSE_SUPPORT)
    SET(SSE_SUPPORT 0)
ENDIF()
ADD_DEFINITIONS(-DSSE_SUPPORT=${SSE_SUPPORT})

IF (NOT DEFINED DEBUG)
    SET(DEBUG 0)
ENDIF()
ADD_DEFINITIONS(-DDEBUG=${DEBUG})


add_executable(FLEX_h2 src/flex_h2.cpp src/genotype.cpp src/matmult.cpp src/storage.cpp)
