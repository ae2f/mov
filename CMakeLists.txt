cmake_minimum_required(VERSION 3.10)
project(mov VERSION 0.3.1)
enable_testing()
option(ae2f_mov_IS_64 "Would you use the Prm-Vec as 64-bit integer?" OFF)
if(NOT TARGET ${PROJECT_NAME})

add_subdirectory(mod/ae2f/Core)

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

ae2f_CoreLibProjTent(
    ${PROJECT_NAME}
    INTERFACE
    include

    "hin/Int.h.in"
    "include/ae2f/mov/Int.h"

    "hin/Float.h.in"
    "include/ae2f/mov/Float.h"
)

target_link_libraries(${PROJECT_NAME} INTERFACE Core)
ae2f_CoreTestTent(${PROJECT_NAME} test)

endif()