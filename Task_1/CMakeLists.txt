cmake_minimum_required(VERSION 3.22)
project("Task_1")

find_package(GTest REQUIRED)

set(CLANG_TIDY_COMMAND "/usr/bin/clang-tidy")
set(CLANG_TIDY_CHECKS "readability-*,modernize-*")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fsanitize=address -fno-omit-frame-pointer") #-fsanitize=thread

add_custom_target(
    lint
    COMMAND ${CLANG_TIDY_COMMAND} --checks=${CLANG_TIDY_CHECKS} --format-style=file ${CMAKE_SOURCE_DIR}/*.cpp
    COMMENT "RUNNING CLANG_TIDY" 
)

add_executable(Task Task_1.cpp)

add_dependencies(Task lint)

target_link_libraries(Task ${GTEST_LIBRARIES})

enable_testing()
add_test(Task_1 Task)

