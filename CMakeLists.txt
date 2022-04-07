cmake_minimum_required(VERSION 3.5)
project(intgemm_fallback)

if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Release)
endif()

set(CMAKE_CXX_STANDARD 11)


set(COMPILE_WASM 1)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -msimd128 -mssse3 -O3")
set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -Wl,--no-entry,--import-memory")
set(CMAKE_EXECUTABLE_SUFFIX ".wasm")

add_subdirectory(intgemm EXCLUDE_FROM_ALL)

add_executable(intgemm_fallback src/fallback.cpp)
target_link_libraries(intgemm_fallback intgemm)

