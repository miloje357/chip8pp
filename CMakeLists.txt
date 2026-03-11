cmake_minimum_required(VERSION 3.23)
project(chip8pp VERSION 0.1.0 LANGUAGES CXX)
set(APP_ID "com.miloje357.chip8pp")
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

configure_file(${CMAKE_CURRENT_SOURCE_DIR}/config.h.in ${CMAKE_CURRENT_BINARY_DIR}/config.h)

option(MYGAME_VENDORED "Use vendored libraries" OFF)

if(MYGAME_VENDORED)
    add_subdirectory(vendored/SDL EXCLUDE_FROM_ALL)
else()
    find_package(SDL3 REQUIRED CONFIG REQUIRED COMPONENTS SDL3-shared)
endif()

add_executable(chip8pp src/main.cpp)

target_link_libraries(chip8pp PRIVATE SDL3::SDL3)
target_include_directories(chip8pp PRIVATE ${CMAKE_CURRENT_BINARY_DIR})
