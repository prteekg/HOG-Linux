cmake_minimum_required (VERSION 2.6)

project (HOG_Linux_cmake)
include(FindPkgConfig)

FIND_PACKAGE( Boost 1.40 COMPONENTS program_options REQUIRED )
INCLUDE_DIRECTORIES( ${Boost_INCLUDE_DIR} )

find_package(X11 REQUIRED)

message(STATUS "X11_FOUND = ${X11_FOUND}")
message(STATUS "X11_INCLUDE_DIR = ${X11_INCLUDE_DIR}")
message(STATUS "X11_LIBRARIES = ${X11_LIBRARIES}")
include_directories(${X11_INCLUDE_DIR})
link_directories(${X11_LIBRARIES})

set(THREADS_PREFER_PTHREAD_FLAG ON)
find_package(Threads REQUIRED)

add_executable(bin/hog hog.cpp integral_histogram.cpp hog_extractor.cpp)

SET(CMAKE_CXX_FLAGS "-O3 -I")

target_link_libraries(bin/hog Threads::Threads ${X11_LIBRARIES} ${Boost_LIBRARIES})

