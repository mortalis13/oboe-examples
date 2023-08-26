#
# Copyright 2019 The Android Open Source Project
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
project(drumthumper LANGUAGES CXX)

find_package(oboe REQUIRED CONFIG)

set (APP_SOURCES
        DrumPlayerJNI.cpp
        player/SampleSource.cpp
        player/SampleBuffer.cpp
        player/OneShotSampleSource.cpp
        player/SimpleMultiPlayer.cpp
        stream/FileInputStream.cpp
        stream/InputStream.cpp
        stream/MemInputStream.cpp
        wav/AudioEncoding.cpp
        wav/WavChunkHeader.cpp
        wav/WavFmtChunkHeader.cpp
        wav/WavRIFFChunkHeader.cpp
        wav/WavStreamReader.cpp
        resampler/IntegerRatio.cpp
        resampler/LinearResampler.cpp
        resampler/MultiChannelResampler.cpp
        resampler/PolyphaseResampler.cpp
        resampler/PolyphaseResamplerMono.cpp
        resampler/PolyphaseResamplerStereo.cpp
        resampler/SincResampler.cpp
        resampler/SincResamplerStereo.cpp
        )


include_directories(
        ${CMAKE_CURRENT_LIST_DIR}
        )


add_library(drumthumper SHARED
        ${APP_SOURCES}
        )

target_compile_options(drumthumper PRIVATE -w -Wno-unused-variable "$<$<CONFIG:RELEASE>:-Ofast>")

target_link_libraries( # Specifies the target library.
        drumthumper

        -Wl,--whole-archive
        -Wl,--no-whole-archive

        oboe::oboe

        # Links the target library to the log library
        # included in the NDK.
        log)
