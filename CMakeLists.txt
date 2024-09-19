cmake_minimum_required(VERSION 3.27)
project(geometryhpp VERSION 1.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_library(geometryhpp INTERFACE)

target_include_directories(geometryhpp
  INTERFACE
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:include>
)

include(CMakePackageConfigHelpers)
configure_package_config_file(
  "${CMAKE_CURRENT_SOURCE_DIR}/geometryhppConfig.cmake.in"
  "${CMAKE_CURRENT_BINARY_DIR}/geometryhppConfig.cmake"
  INSTALL_DESTINATION share/geometryhpp
)

install(TARGETS geometryhpp
  EXPORT geometryhppTargets
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
  RUNTIME DESTINATION bin
)

install(DIRECTORY
  "${CMAKE_CURRENT_SOURCE_DIR}/include/mapbox"
  DESTINATION include
)

install(
  EXPORT geometryhppTargets
  DESTINATION share/geometryhpp
  NAMESPACE geometryhpp::
)

install(
  FILES
  "${CMAKE_CURRENT_BINARY_DIR}/geometryhppConfig.cmake"
  DESTINATION share/geometryhpp
)