cmake_minimum_required(VERSION 3.25)
project(ConanCMakeDemo)

add_definitions("-std=c++11")

include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
conan_basic_setup()

add_executable(${PROJECT_NAME} boostHello.cpp)
target_link_libraries(${PROJECT_NAME} ${CONAN_LIBS})
