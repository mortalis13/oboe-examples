#
# Copyright 2017 The Android Open Source Project
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#

cmake_minimum_required(VERSION 3.4.1)
# project(hello-oboe LANGUAGES CXX)

find_package(oboe REQUIRED CONFIG)

include_directories(${CMAKE_CURRENT_LIST_DIR}/debug-utils)
include_directories(${CMAKE_CURRENT_LIST_DIR}/shared)

# Build the libhello-oboe library
add_library(hello-oboe SHARED
  jni_bridge.cpp
  HelloOboeEngine.cpp
  SoundGenerator.cpp
  LatencyTuningCallback.cpp

  debug-utils/trace.cpp
)

# Specify the libraries needed for hello-oboe
target_link_libraries(hello-oboe oboe::oboe android log)

# Enable optimization flags: if having problems with source level debugging,
# disable -Ofast ( and debug ), re-enable after done debugging.
target_compile_options(hello-oboe PRIVATE -Wall -Werror "$<$<CONFIG:RELEASE>:-Ofast>")
