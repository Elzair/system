cmake_minimum_required(VERSION 3.3)

project(boost_system)

option(BOOST_SYSTEM_SHARED_LIB "Enable dynamic linking" ON)

set(SOURCE_FILES src/error_code.cpp)

if(BOOST_SYSTEM_SHARED_LIB)
  add_library(boost_system SHARED ${SOURCE_FILES} )
  target_compile_definitions(boost_system PRIVATE BOOST_SYSTEM_DYN_LINK=1)
else()
  add_library(boost_system STATIC ${SOURCE_FILES})
  target_compile_definitions(boost_system PRIVATE BOOST_SYSTEM_STATIC_LINK=1)
endif(BOOST_SYSTEM_SHARED_LIB)

target_include_directories(boost_system BEFORE PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)
target_link_libraries(boost_system boost_predef boost_config boost_assert boost_core)

install(TARGETS boost_system DESTINATION lib)
install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/include/boost DESTINATION include)

add_library(boost::system ALIAS boost_system)
