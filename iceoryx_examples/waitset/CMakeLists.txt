# Copyright (c) 2020 by Apex.AI Inc. All rights reserved.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

cmake_minimum_required(VERSION 3.5)
project(example_waitset)

include(GNUInstallDirs)

find_package(iceoryx_posh CONFIG REQUIRED)

get_target_property(ICEORYX_CXX_STANDARD iceoryx_posh::iceoryx_posh CXX_STANDARD)
if ( NOT ICEORYX_CXX_STANDARD )
    include(IceoryxPlatformDetection)
endif ( NOT ICEORYX_CXX_STANDARD )

add_executable(iox-ex-publisher-waitset ./ice_publisher_waitset.cpp)
target_link_libraries(iox-ex-publisher-waitset
    iceoryx_posh::iceoryx_posh
)
set_target_properties(iox-ex-publisher-waitset PROPERTIES
    CXX_STANDARD_REQUIRED ON
    CXX_STANDARD ${ICEORYX_CXX_STANDARD}
    POSITION_INDEPENDENT_CODE ON
)

add_executable(iox-ex-subscriber-waitset ./ice_subscriber_waitset.cpp)
target_link_libraries(iox-ex-subscriber-waitset
    iceoryx_posh::iceoryx_posh
)
set_target_properties(iox-ex-subscriber-waitset PROPERTIES
    CXX_STANDARD_REQUIRED ON
    CXX_STANDARD ${ICEORYX_CXX_STANDARD}
    POSITION_INDEPENDENT_CODE ON
)

install(
    TARGETS iox-ex-publisher-waitset iox-ex-subscriber-waitset
    RUNTIME DESTINATION bin
)
