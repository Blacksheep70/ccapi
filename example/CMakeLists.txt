cmake_minimum_required(VERSION 3.14)
set(NAME example)
project(${NAME})
set(CMAKE_CXX_STANDARD 14)
if(NOT APPLE AND NOT MSVC)
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -pthread")
endif()
get_filename_component(CCAPI_CPP_PROJECT_DIR ../ ABSOLUTE)
message(STATUS "CCAPI_CPP_PROJECT_DIR: ${CCAPI_CPP_PROJECT_DIR}")
set(RAPIDJSON_INCLUDE_DIR ${CCAPI_CPP_PROJECT_DIR}/dependency/rapidjson/include)
set(WEBSOCKETPP_INCLUDE_DIR ${CCAPI_CPP_PROJECT_DIR}/dependency/websocketpp)
set(BOOST_INCLUDE_DIR ${CCAPI_CPP_PROJECT_DIR}/dependency/boost)
set(DATE_INCLUDE_DIR ${CCAPI_CPP_PROJECT_DIR}/dependency/date/include)
find_package(OpenSSL REQUIRED)
include_directories(${CCAPI_CPP_PROJECT_DIR}/include ${WEBSOCKETPP_INCLUDE_DIR} ${BOOST_INCLUDE_DIR} ${RAPIDJSON_INCLUDE_DIR} ${DATE_INCLUDE_DIR} ${OPENSSL_INCLUDE_DIR})
set(ADDITIONAL_LINK_LIBRARIES "")
if (WIN32)
  set(ADDITIONAL_LINK_LIBRARIES ws2_32)
endif()
link_libraries(OpenSSL::Crypto OpenSSL::SSL ${ADDITIONAL_LINK_LIBRARIES})
add_subdirectory(src/market_data_simple)
add_subdirectory(src/market_data_trades)
add_subdirectory(src/market_data_advanced)
add_subdirectory(src/execution_management_simple)
add_subdirectory(src/execution_management_complex)
add_subdirectory(src/market_making)
add_subdirectory(src/cross_exchange_arbitrage)
add_subdirectory(src/enable_library_logging)
