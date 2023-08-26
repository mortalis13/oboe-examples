cmake_minimum_required(VERSION 3.4.1)
project(megadrone LANGUAGES CXX)

find_package(oboe REQUIRED CONFIG)

add_library( megadrone SHARED
  native-lib.cpp
  MegaDroneEngine.cpp
  
  debug-utils/trace.cpp
)

include_directories(
  shared
  debug-utils
)

target_link_libraries( megadrone log oboe::oboe )
