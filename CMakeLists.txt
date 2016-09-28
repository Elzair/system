if(APPLE)
  cmake_minimum_required(VERSION 2.8.11 FATAL_ERROR)
else()
  cmake_minimum_required(VERSION 2.8.7 FATAL_ERROR)
endif()

option(BOOST_SYSTEM_SHARED_LIB "Enable dynamic linking" ON)

set(SOURCE_FILES src/error_code.cpp)

if(BOOST_SYSTEM_SHARED_LIB)
  add_library(boost_system SHARED GLOBAL ${SOURCE_FILES} )
  target_compile_definitions(boost_system PRIVATE BOOST_SYSTEM_DYN_LINK=1)
else()
  add_library(boost_system STATIC GLOBAL ${SOURCE_FILES})
  target_compile_definitions(boost_system PRIVATE BOOST_SYSTEM_STATIC_LINK=1)
endif(BOOST_SYSTEM_SHARED_LIB)

target_include_directories(boost_system BEFORE PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)
