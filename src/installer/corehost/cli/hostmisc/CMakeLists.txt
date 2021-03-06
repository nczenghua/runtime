# Licensed to the .NET Foundation under one or more agreements.
# The .NET Foundation licenses this file to you under the MIT license.
# See the LICENSE file in the project root for more information.

project(hostmisc)

set(DOTNET_PROJECT_NAME "hostmisc")

# CMake does not recommend using globbing since it messes with the freshness checks
set(SOURCES
    trace.cpp
    utils.cpp
    ../fxr/fx_ver.cpp
)

set(HEADERS
    trace.h
    utils.h
    pal.h
    ../../error_codes.h
    ../fxr/fx_ver.h
)

if(CLR_CMAKE_TARGET_WIN32)
    list(APPEND SOURCES
        pal.windows.cpp
        longfile.windows.cpp)
    list(APPEND HEADERS
        longfile.h)
else()
    list(APPEND SOURCES
        pal.unix.cpp
        ${VERSION_FILE_PATH})
endif()

set(SKIP_VERSIONING 1)
include(../lib_static.cmake)

