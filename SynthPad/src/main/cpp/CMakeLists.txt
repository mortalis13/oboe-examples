cmake_minimum_required(VERSION 3.4.1)
project(soundboard LANGUAGES CXX)

find_package(oboe REQUIRED CONFIG)

include_directories(shared debug-utils)

add_library( soundboard SHARED native-lib.cpp SoundBoardEngine.cpp )

target_link_libraries( soundboard log oboe::oboe )
