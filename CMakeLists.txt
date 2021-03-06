cmake_minimum_required (VERSION 3.1.3)
project (dtdump)
SET(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${PROJECT_SOURCE_DIR}/cmake/")

find_package(LibSndFile REQUIRED)
find_package(LibUSB REQUIRED)

if(LIBSNDFILE_FOUND)
    message(STATUS "LIBSNDFILE_INCLUDE_DIR='${LIBSNDFILE_INCLUDE_DIR}'")
    message(STATUS "LIBSNDFILE_LIBRARY=${LIBSNDFILE_LIBRARY}")
    include_directories(${LIBSNDFILE_INCLUDE_DIR})
else()
	message(STATUS "LIBSNDFILE not found!")
endif(LIBSNDFILE_FOUND)

if(LibUSB_FOUND)
	message(STATUS "LibUSB_INCLUDE_DIRS='${LibUSB_INCLUDE_DIRS}'")
    message(STATUS "LibUSB_LIBRARIES=${LibUSB_LIBRARIES}")
    include_directories(${LibUSB_INCLUDE_DIRS})
else()
	message(STATUS "LibUSB not found!")
endif(LibUSB_FOUND)

include_directories(header)
file(GLOB SOURCES "src/*.c")

add_executable(dtdump ${SOURCES})  
target_link_libraries(dtdump ${LibUSB_LIBRARIES} ${LIBSNDFILE_LIBRARY} pthread)
set_property(TARGET dtdump PROPERTY C_STANDARD 99)