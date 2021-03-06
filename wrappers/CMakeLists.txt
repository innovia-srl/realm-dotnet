cmake_minimum_required(VERSION 3.4.0)

set(CMAKE_BUILD_TYPE Debug CACHE STRING "")
project(realm-wrappers)

list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/src/object-store/CMake")

include(CompilerFlags)

set(REALM_ENABLE_SYNC OFF CACHE BOOL "")

include(RealmCore)
use_realm_core("${REALM_ENABLE_SYNC}" "${REALM_CORE_PREFIX}" "${REALM_SYNC_PREFIX}")

if(APPLE)
  set(CMAKE_OSX_DEPLOYMENT_TARGET 10.10)
endif()

if(REALM_ENABLE_SYNC)
  add_definitions(-DREALM_ENABLE_SYNC)
endif()

set(PEGTL_INCLUDE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/src/object-store/external/pegtl)

add_subdirectory(src/object-store/src)
add_subdirectory(src)