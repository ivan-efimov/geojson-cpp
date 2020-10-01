cmake_minimum_required(VERSION 3.0)
project(geojson-cpp)

if (NOT MAPBOX_VARIANT_INCLUDE_DIR)
	message(SEND_ERROR "MAPBOX_VARIANT_INCLUDE_DIR is required by geojson-cpp but not defined")
endif ()
if (NOT MAPBOX_GEOMETRY_INCLUDE_DIR)
	message(SEND_ERROR "MAPBOX_GEOMETRY_INCLUDE_DIR is required by geojson-cpp but not defined")
endif ()
if (NOT RAPIDJSON_INCLUDE_DIR)
	message(SEND_ERROR "RAPIDJSON_INCLUDE_DIR is required by geojson-cpp but not defined")
endif ()

add_library(geojson-cpp_static STATIC ${CMAKE_CURRENT_SOURCE_DIR}/src/mapbox/geojson.cpp)
target_include_directories(geojson-cpp_static PUBLIC
	${CMAKE_CURRENT_SOURCE_DIR}/include
	${MAPBOX_VARIANT_INCLUDE_DIR}
	${MAPBOX_GEOMETRY_INCLUDE_DIR}
	${RAPIDJSON_INCLUDE_DIR}
)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++14 -Wall -Wextra -Wshadow -O3 -fPIC")
set(CMAKE_C_FLAGS ${CMAKE_C_FLAGS} "-fvisibility=hidden")