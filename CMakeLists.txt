cmake_minimum_required(VERSION 3.10)
project(mov VERSION 0.7.4)
enable_testing()
option(ae2f_mov_IS_64 "Would you use the Prm-Vec as 64-bit integer?" OFF)
if(NOT TARGET ${PROJECT_NAME})

include(cmake/Core.cmake)
ae2f_CoreLibFetch(ae2f Core Rel-v6.15.11)

if(ae2f_float STREQUAL "float")
set(ae2f_float_id 0)
elseif(ae2f_float STREQUAL "double")
set(ae2f_float_id 1)
elseif(ae2f_float STREQUAL "long double")
set(ae2f_float_id 2)
endif()

configure_file(${PROJECT_SOURCE_DIR}/hin/Int.h.in ${PROJECT_SOURCE_DIR}/include/ae2f/mov/Int.h)
configure_file(${PROJECT_SOURCE_DIR}/hin/Float.h.in ${PROJECT_SOURCE_DIR}/include/ae2f/mov/Float.h)

unset(ae2f_float_id)


# Namespace Package
include(GNUInstallDirs)

ae2f_CoreLibTent(
    ${PROJECT_NAME} INTERFACE
    include ae2f

    "hin/Int.h.in"
    "include/ae2f/mov/Int.h"

    "hin/Float.h.in"
    "include/ae2f/mov/Float.h"
)

ae2f_CoreUtilityDocTent(${PROJECT_NAME} cmake ae2f Core)

target_link_libraries(${PROJECT_NAME} INTERFACE Core)
ae2f_CoreTestTent(${PROJECT_NAME} test)

endif()