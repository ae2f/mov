link_libraries(mov)
project(movTest)

add_executable(${PROJECT_NAME} "main.c")
add_test(NAME ${PROJECT_NAME} COMMAND ${PROJECT_NAME})