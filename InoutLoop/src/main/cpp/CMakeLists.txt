#
# Copyright 2018 The Android Open Source Project
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
project(liveEffect LANGUAGES C CXX)

find_package(oboe REQUIRED CONFIG)

add_library(liveEffect SHARED
    LiveEffectEngine.cpp
    FullDuplexStream.cpp
    jni_bridge.cpp
    
    debug-utils/trace.cpp
)

include_directories(
  ${CMAKE_CURRENT_LIST_DIR}/debug-utils
)

target_link_libraries(liveEffect PRIVATE
    oboe::oboe
    android
    atomic
    log
)
