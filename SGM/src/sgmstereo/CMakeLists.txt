project(sgmstereo CXX)

################################################################################
# Source groups
################################################################################
set(Headers
    "dsimage.h"
    "sgmstereo.h"
)
source_group("Headers" FILES ${Headers})

set(Sources
    "dsimage.cpp"
    "sgmstereo.cpp"
)
source_group("Sources" FILES ${Sources})

set(ALL_FILES
    ${Headers}
    ${Sources}
)

################################################################################
# Target
################################################################################
add_library(${PROJECT_NAME} STATIC ${ALL_FILES})

use_props(${PROJECT_NAME} "${CMAKE_CONFIGURATION_TYPES}" "${DEFAULT_CXX_PROPS}")
################################################################################
# Includes for CMake from *.props
################################################################################
use_props(${PROJECT_NAME} "${CMAKE_CONFIGURATION_TYPES}" "$([MSBuild]::GetDirectoryNameOfFileAbove($(MSBuildThisFileDirectory), AirSim.cmake))/AirSim.cmake")

set(ROOT_NAMESPACE Features)

################################################################################
# Output directory
################################################################################
if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "Any CPU")
    set_target_properties(${PROJECT_NAME} PROPERTIES
        OUTPUT_DIRECTORY_DEBUG   "${CMAKE_CURRENT_SOURCE_DIR}/../../lib/$ENV{PlatformToolset}/${CMAKE_VS_PLATFORM_NAME}/$<CONFIG>/"
        OUTPUT_DIRECTORY_RELEASE "${CMAKE_CURRENT_SOURCE_DIR}/../../lib/$ENV{PlatformToolset}/${CMAKE_VS_PLATFORM_NAME}/$<CONFIG>/"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "ARM")
    set_target_properties(${PROJECT_NAME} PROPERTIES
        OUTPUT_DIRECTORY_DEBUG   "${CMAKE_CURRENT_SOURCE_DIR}/../../lib/$ENV{PlatformToolset}/${CMAKE_VS_PLATFORM_NAME}/$<CONFIG>/"
        OUTPUT_DIRECTORY_RELEASE "${CMAKE_CURRENT_SOURCE_DIR}/../../lib/$ENV{PlatformToolset}/${CMAKE_VS_PLATFORM_NAME}/$<CONFIG>/"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
    set_target_properties(${PROJECT_NAME} PROPERTIES
        OUTPUT_DIRECTORY_DEBUG   "${CMAKE_CURRENT_SOURCE_DIR}/../../lib/$ENV{PlatformToolset}/${CMAKE_VS_PLATFORM_NAME}/$<CONFIG>/"
        OUTPUT_DIRECTORY_RELEASE "${CMAKE_CURRENT_SOURCE_DIR}/../../lib/$ENV{PlatformToolset}/${CMAKE_VS_PLATFORM_NAME}/$<CONFIG>/"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
    set_target_properties(${PROJECT_NAME} PROPERTIES
        OUTPUT_DIRECTORY_DEBUG   "${CMAKE_CURRENT_SOURCE_DIR}/../../lib/$ENV{PlatformToolset}/${CMAKE_VS_PLATFORM_NAME}/$<CONFIG>/"
        OUTPUT_DIRECTORY_RELEASE "${CMAKE_CURRENT_SOURCE_DIR}/../../lib/$ENV{PlatformToolset}/${CMAKE_VS_PLATFORM_NAME}/$<CONFIG>/"
    )
endif()
if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "Any CPU")
    set_target_properties(${PROJECT_NAME} PROPERTIES
        INTERPROCEDURAL_OPTIMIZATION_RELEASE "TRUE"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "ARM")
    set_target_properties(${PROJECT_NAME} PROPERTIES
        INTERPROCEDURAL_OPTIMIZATION_RELEASE "TRUE"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
    set_target_properties(${PROJECT_NAME} PROPERTIES
        INTERPROCEDURAL_OPTIMIZATION_RELEASE "TRUE"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
    set_target_properties(${PROJECT_NAME} PROPERTIES
        INTERPROCEDURAL_OPTIMIZATION_RELEASE "TRUE"
    )
endif()
################################################################################
# Include directories
################################################################################
if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "Any CPU")
    target_include_directories(${PROJECT_NAME} PUBLIC
        "${CMAKE_CURRENT_SOURCE_DIR}/VRLib/inc/VRLibCore;"
        "${CMAKE_CURRENT_SOURCE_DIR}/VRLib/inc/VRLibCV;"
        "${CMAKE_CURRENT_SOURCE_DIR}/VRLib/inc/VRLibImageIO;"
        "${CMAKE_CURRENT_SOURCE_DIR}/LibJpeg/inc;"
        "${CMAKE_CURRENT_SOURCE_DIR}/LibTiff/inc"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "ARM")
    target_include_directories(${PROJECT_NAME} PUBLIC
        "${CMAKE_CURRENT_SOURCE_DIR}/VRLib/inc/VRLibCore;"
        "${CMAKE_CURRENT_SOURCE_DIR}/VRLib/inc/VRLibCV;"
        "${CMAKE_CURRENT_SOURCE_DIR}/VRLib/inc/VRLibImageIO;"
        "${CMAKE_CURRENT_SOURCE_DIR}/LibJpeg/inc;"
        "${CMAKE_CURRENT_SOURCE_DIR}/LibTiff/inc"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
    target_include_directories(${PROJECT_NAME} PUBLIC
        "${CMAKE_CURRENT_SOURCE_DIR}/VRLib/inc/VRLibCore;"
        "${CMAKE_CURRENT_SOURCE_DIR}/VRLib/inc/VRLibCV;"
        "${CMAKE_CURRENT_SOURCE_DIR}/VRLib/inc/VRLibImageIO;"
        "${CMAKE_CURRENT_SOURCE_DIR}/LibJpeg/inc;"
        "${CMAKE_CURRENT_SOURCE_DIR}/LibTiff/inc"
    )
endif()

################################################################################
# Compile definitions
################################################################################
if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "Any CPU")
    target_compile_definitions(${PROJECT_NAME} PRIVATE
        "VRLIB_USES_LIBTIFF;"
        "VRLIB_USES_LIBJPEG;"
        "NOMINMAX;"
        "_UNICODE;"
        "UNICODE"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "ARM")
    target_compile_definitions(${PROJECT_NAME} PRIVATE
        "VRLIB_USES_LIBTIFF;"
        "VRLIB_USES_LIBJPEG;"
        "NOMINMAX;"
        "_UNICODE;"
        "UNICODE"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
    target_compile_definitions(${PROJECT_NAME} PRIVATE
        "NOMINMAX;"
        "_UNICODE;"
        "UNICODE"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
    target_compile_definitions(${PROJECT_NAME} PRIVATE
        "VRLIB_USES_LIBTIFF;"
        "VRLIB_USES_LIBJPEG;"
        "NOMINMAX;"
        "_UNICODE;"
        "UNICODE"
    )
endif()

################################################################################
# Compile and link options
################################################################################
if(MSVC)
    if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "Any CPU")
        target_compile_options(${PROJECT_NAME} PRIVATE
            $<$<CONFIG:Debug>:
                /Gm;
                /Od;
                /RTC1;
                /MDd
            >
            $<$<CONFIG:Release>:
                /GL-;
                /O2;
                /MD
            >
            /W4;
            /WX-;
            /Zi;
            ${DEFAULT_CXX_EXCEPTION_HANDLING};
            /openmp
        )
    elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "ARM")
        target_compile_options(${PROJECT_NAME} PRIVATE
            $<$<CONFIG:Debug>:
                /Gm;
                /Od;
                /RTC1;
                /MDd
            >
            $<$<CONFIG:Release>:
                /GL-;
                /O2;
                /MD
            >
            /W4;
            /WX-;
            /Zi;
            ${DEFAULT_CXX_EXCEPTION_HANDLING};
            /openmp
        )
    elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
        target_compile_options(${PROJECT_NAME} PRIVATE
            $<$<CONFIG:Debug>:
                /Od;
                /RTC1;
                /MDd
            >
            $<$<CONFIG:Release>:
                /GL-;
                /O2;
                /MD;
                /Gy
            >
            /W4;
            /Zi;
            ${DEFAULT_CXX_EXCEPTION_HANDLING};
            /openmp
        )
    elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
        target_compile_options(${PROJECT_NAME} PRIVATE
            $<$<CONFIG:Debug>:
                /Gm;
                /Od;
                /RTC1;
                /MDd
            >
            $<$<CONFIG:Release>:
                /GL-;
                /O2;
                /MD
            >
            /W4;
            /WX-;
            /Zi;
            ${DEFAULT_CXX_EXCEPTION_HANDLING};
            /openmp
        )
    endif()
endif()

