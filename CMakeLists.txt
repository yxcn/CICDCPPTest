cmake_minimum_required(VERSION 3.16)
project(CICDCPPTest LANGUAGES CXX)

enable_testing()

add_library(core src/add.cpp)
target_include_directories(core PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)

add_executable(app src/main.cpp)
target_link_libraries(app PRIVATE core)

add_executable(test_add test/test.cpp)
target_link_libraries(test_add PRIVATE core)

add_test(NAME AddTest COMMAND test_add)

target_compile_features(core PUBLIC cxx_std_17)

if (CMAKE_CXX_COMPILER_ID MATCHES "GNU|Clang")
  target_compile_options(core PRIVATE -Wall -Wextra -Wpedantic -Werror)
endif()