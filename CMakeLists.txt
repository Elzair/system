if(APPLE)
  cmake_minimum_required(VERSION 2.8.11 FATAL_ERROR)
else()
  cmake_minimum_required(VERSION 2.8.7 FATAL_ERROR)
endif()

if(NOT BOOST_CONFIG_INCLUDE_DIRS)
  message(FATAL_ERROR "Cannot find boost.config!")
endif(NOT BOOST_CONFIG_INCLUDE_DIRS)

option(BOOST_SHARED_LIB "Enable dynamic linking" ON)

set(BOOST_SYSTEM_INCLUDE_DIRS "${CMAKE_CURRENT_SOURCE_DIR}/include" CACHE STRING "Location of boost.system headers")

set(BOOST_INCLUDE_DIRS "${BOOST_INCLUDE_DIRS}" "${BOOST_SYSTEM_INCLUDE_DIRS}" CACHE STRING "All Boost headers" FORCE)

include_directories(${BOOST_INCLUDE_DIRS})

project(boost_system)

set(SOURCE_FILES src/error_code.cpp)

if(BOOST_SHARED_LIB)
  add_definitions(-DBOOST_SYSTEM_DYN_LINK=1)
  add_library(boost_system SHARED ${SOURCE_FILES})
else()
  add_definitions(-DBOOST_SYSTEM_STATIC_LINK=1)
  add_library(boost_system STATIC ${SOURCE_FILES})
endif(BOOST_SHARED_LIB)

if("${CMAKE_CXX_COMPILER_ID}" STREQUAL "Clang" OR "${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU")
  set(BOOST_SYSTEM_LIBRARIES "-L ${CMAKE_CURRENT_BINARY_DIR} -lboost_system" CACHE STRING "Location of boost.system library")
  
  if(NOT BOOST_LIBRARIES)
    set(BOOST_LIBRARIES "${BOOST_SYSTEM_LIBRARIES}" CACHE STRING "All Boost libraries")
  else()
    set(BOOST_LIBRARIES "${BOOST_LIBRARIES}" "${BOOST_SYSTEM_LIBRARIES}" CACHE STRING "All Boost libraries" FORCE)
  endif(NOT BOOST_LIBRARIES)
  
else()
  message(WARNING "You will have to manually link boost_system. BOOST_SYSTEM_LIBRARIES is currently supported only on GCC and Clang.")
endif()
