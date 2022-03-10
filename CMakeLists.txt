cmake_minimum_required(VERSION 3.17.0)

project(p2300_playground LANGUAGES CXX)

include(FetchContent)
FetchContent_Declare(
    wg21_p2300
    GIT_REPOSITORY https://github.com/havogt/wg21_p2300_std_execution.git
    GIT_TAG        consumer_friendly_cmake
)
FetchContent_MakeAvailable(wg21_p2300)

FetchContent_GetProperties(wg21_p2300)
add_library(p2300_examples INTERFACE) # contains schedulers
target_include_directories(p2300_examples INTERFACE ${wg21_p2300_SOURCE_DIR}/examples)

add_executable(hello_world hello_world.cc)
target_link_libraries(hello_world P2300::p2300)

add_executable(on_transfer_with_sleeps on_transfer_with_sleeps.cpp)
target_link_libraries(on_transfer_with_sleeps P2300::p2300 p2300_examples)
