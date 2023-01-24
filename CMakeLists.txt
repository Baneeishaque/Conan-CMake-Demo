cmake_minimum_required(VERSION 3.25)
project(ConanCMakeDemo)

add_definitions("-std=c++11")

if(NOT EXISTS "${CMAKE_BINARY_DIR}/conan.cmake")
  message(STATUS "Downloading conan.cmake from https://github.com/conan-io/cmake-conan")
  file(DOWNLOAD "https://raw.githubusercontent.com/conan-io/cmake-conan/0.18.1/conan.cmake"
                "${CMAKE_BINARY_DIR}/conan.cmake"
                TLS_VERIFY ON)
endif()

include(${CMAKE_BINARY_DIR}/conan.cmake)
conan_cmake_configure(REQUIRES boost/1.81.0
                      GENERATORS cmake)

conan_cmake_install(PATH_OR_REFERENCE .
                    BUILD missing)

include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
conan_basic_setup()

add_executable(${PROJECT_NAME} boostHello.cpp)
target_link_libraries(${PROJECT_NAME} ${CONAN_LIBS})
