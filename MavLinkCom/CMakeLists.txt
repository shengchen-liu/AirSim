project(MavLinkCom CXX)

################################################################################
# Source groups
################################################################################
set(no_group_source_files
    "include/AdHocConnection.hpp"
    "include/UdpSocket.hpp"
    "src/AdHocConnection.cpp"
    "src/impl/AdHocConnectionImpl.cpp"
    "src/impl/AdHocConnectionImpl.hpp"
    "src/impl/UdpSocketImpl.cpp"
    "src/impl/UdpSocketImpl.hpp"
    "src/UdpSocket.cpp"
)
source_group("" FILES ${no_group_source_files})

set(Design
    "Design/Design.dgml"
    "Design/FtpDesign.dgml"
    "Design/OffboardControl.dgml"
)
source_group("Design" FILES ${Design})

set(Mavlink
    "mavlink/checksum.h"
    "mavlink/common/common.h"
    "mavlink/common/mavlink.h"
    "mavlink/common/testsuite.h"
    "mavlink/common/version.h"
    "mavlink/mavlink_conversions.h"
    "mavlink/mavlink_helpers.h"
    "mavlink/mavlink_types.h"
    "mavlink/protocol.h"
)
source_group("Mavlink" FILES ${Mavlink})

set(common_utils
    "common_utils/EnumFlags.hpp"
    "common_utils/ExceptionUtils.hpp"
    "common_utils/FileSystem.cpp"
    "common_utils/FileSystem.hpp"
    "common_utils/json.hpp"
    "common_utils/optional.hpp"
    "common_utils/prettyprint.hpp"
    "common_utils/sincos.hpp"
    "common_utils/StrictMode.hpp"
    "common_utils/ThreadUtils.cpp"
    "common_utils/ThreadUtils.hpp"
    "common_utils/type_utils.hpp"
    "common_utils/Utils.hpp"
)
source_group("common_utils" FILES ${common_utils})

set(include
    "include/AsyncResult.hpp"
    "include/MavLinkConnection.hpp"
    "include/MavLinkFtpClient.hpp"
    "include/MavLinkLog.hpp"
    "include/MavLinkMessageBase.hpp"
    "include/MavLinkMessages.hpp"
    "include/MavLinkNode.hpp"
    "include/MavLinkTcpServer.hpp"
    "include/MavLinkVehicle.hpp"
    "include/MavLinkVideoStream.hpp"
    "include/Semaphore.hpp"
    "include/VehicleState.hpp"
)
source_group("include" FILES ${include})

set(serial_com
    "src/serial_com/Port.h"
    "src/serial_com/SerialPort.cpp"
    "src/serial_com/SerialPort.hpp"
    "src/serial_com/SocketInit.cpp"
    "src/serial_com/SocketInit.hpp"
    "src/serial_com/TcpClientPort.cpp"
    "src/serial_com/TcpClientPort.hpp"
    "src/serial_com/UdpClientPort.cpp"
    "src/serial_com/UdpClientPort.hpp"
    "src/serial_com/wifi.cpp"
    "src/serial_com/wifi.h"
)
source_group("serial_com" FILES ${serial_com})

set(src
    "src/MavLinkConnection.cpp"
    "src/MavLinkFtpClient.cpp"
    "src/MavLinkLog.cpp"
    "src/MavLinkMessageBase.cpp"
    "src/MavLinkMessages.cpp"
    "src/MavLinkNode.cpp"
    "src/MavLinkTcpServer.cpp"
    "src/MavLinkVehicle.cpp"
    "src/MavLinkVideoStream.cpp"
    "src/Semaphore.cpp"
)
source_group("src" FILES ${src})

set(src__impl
    "src/impl/MavLinkConnectionImpl.cpp"
    "src/impl/MavLinkConnectionImpl.hpp"
    "src/impl/MavLinkFtpClientImpl.cpp"
    "src/impl/MavLinkFtpClientImpl.hpp"
    "src/impl/MavLinkNodeImpl.cpp"
    "src/impl/MavLinkNodeImpl.hpp"
    "src/impl/MavLinkTcpServerImpl.cpp"
    "src/impl/MavLinkTcpServerImpl.hpp"
    "src/impl/MavLinkVehicleImpl.cpp"
    "src/impl/MavLinkVehicleImpl.hpp"
    "src/impl/MavLinkVideoStreamImpl.cpp"
    "src/impl/MavLinkVideoStreamImpl.hpp"
)
source_group("src\\impl" FILES ${src__impl})

set(src__impl__onecore
    "src/impl/onecore/OneCoreFindSerialPorts.cpp"
)
source_group("src\\impl\\onecore" FILES ${src__impl__onecore})

set(src__impl__windows
    "src/impl/windows/WindowsFindSerialPorts.cpp"
)
source_group("src\\impl\\windows" FILES ${src__impl__windows})

set(ALL_FILES
    ${no_group_source_files}
    ${Design}
    ${Mavlink}
    ${common_utils}
    ${include}
    ${serial_com}
    ${src}
    ${src__impl}
    ${src__impl__onecore}
    ${src__impl__windows}
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

set(ROOT_NAMESPACE PX4_P)

set_target_properties(${PROJECT_NAME} PROPERTIES
    VS_GLOBAL_KEYWORD "Win32Proj"
)
################################################################################
# Output directory
################################################################################
if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "Any CPU")
    set_target_properties(${PROJECT_NAME} PROPERTIES
        OUTPUT_DIRECTORY_DEBUG   "${CMAKE_CURRENT_SOURCE_DIR}/lib/${CMAKE_VS_PLATFORM_NAME}/$<CONFIG>/"
        OUTPUT_DIRECTORY_RELEASE "${CMAKE_CURRENT_SOURCE_DIR}/lib/${CMAKE_VS_PLATFORM_NAME}/$<CONFIG>/"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "ARM")
    set_target_properties(${PROJECT_NAME} PROPERTIES
        OUTPUT_DIRECTORY_DEBUG   "${CMAKE_CURRENT_SOURCE_DIR}/lib/${CMAKE_VS_PLATFORM_NAME}/$<CONFIG>/"
        OUTPUT_DIRECTORY_RELEASE "${CMAKE_CURRENT_SOURCE_DIR}/lib/${CMAKE_VS_PLATFORM_NAME}/$<CONFIG>/"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
    set_target_properties(${PROJECT_NAME} PROPERTIES
        OUTPUT_DIRECTORY_DEBUG   "${CMAKE_CURRENT_SOURCE_DIR}/lib/${CMAKE_VS_PLATFORM_NAME}/$<CONFIG>/"
        OUTPUT_DIRECTORY_RELEASE "${CMAKE_CURRENT_SOURCE_DIR}/lib/${CMAKE_VS_PLATFORM_NAME}/$<CONFIG>/"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
    set_target_properties(${PROJECT_NAME} PROPERTIES
        OUTPUT_DIRECTORY_DEBUG   "${CMAKE_CURRENT_SOURCE_DIR}/lib/${CMAKE_VS_PLATFORM_NAME}/$<CONFIG>/"
        OUTPUT_DIRECTORY_RELEASE "${CMAKE_CURRENT_SOURCE_DIR}/lib/${CMAKE_VS_PLATFORM_NAME}/$<CONFIG>/"
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
        INTERPROCEDURAL_OPTIMIZATION_RELEASE "FALSE"
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
        "${CMAKE_CURRENT_SOURCE_DIR}/common_utils;"
        "${CMAKE_CURRENT_SOURCE_DIR}/include"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "ARM")
    target_include_directories(${PROJECT_NAME} PUBLIC
        "${CMAKE_CURRENT_SOURCE_DIR}/common_utils;"
        "${CMAKE_CURRENT_SOURCE_DIR}/include"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
    target_include_directories(${PROJECT_NAME} PUBLIC
        "${CMAKE_CURRENT_SOURCE_DIR}/common_utils;"
        "${CMAKE_CURRENT_SOURCE_DIR}/include"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
    target_include_directories(${PROJECT_NAME} PUBLIC
        "${CMAKE_CURRENT_SOURCE_DIR}/common_utils;"
        "${CMAKE_CURRENT_SOURCE_DIR}/include"
    )
endif()

################################################################################
# Compile definitions
################################################################################
if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "Any CPU")
    target_compile_definitions(${PROJECT_NAME} PRIVATE
        "$<$<CONFIG:Debug>:"
            "_DEBUG"
        ">"
        "_WIN32_WINNT=0x0600;"
        "_WIN32;"
        "WIN32;"
        "_SCL_SECURE_NO_WARNINGS;"
        "_CRT_SECURE_NO_WARNINGS;"
        "_LIB;"
        "UNICODE;"
        "_UNICODE"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "ARM")
    target_compile_definitions(${PROJECT_NAME} PRIVATE
        "$<$<CONFIG:Debug>:"
            "_DEBUG"
        ">"
        "ONECORE;"
        "_WIN32_WINNT=0x0600;"
        "_WIN32;"
        "WIN32;"
        "_SCL_SECURE_NO_WARNINGS;"
        "_CRT_SECURE_NO_WARNINGS;"
        "_LIB;"
        "UNICODE;"
        "_UNICODE"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
    target_compile_definitions(${PROJECT_NAME} PRIVATE
        "$<$<CONFIG:Debug>:"
            "_DEBUG"
        ">"
        "$<$<CONFIG:Release>:"
            "_CRT_NONSTDC_NO_DEPRECATE"
        ">"
        "_WIN32;"
        "_WIN32_WINNT=0x0600;"
        "NOMINMAX;"
        "VC_EXTRALEAN;"
        "_SCL_SECURE_NO_WARNINGS;"
        "_CRT_SECURE_NO_WARNINGS;"
        "_LIB;"
        "UNICODE;"
        "_UNICODE"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
    target_compile_definitions(${PROJECT_NAME} PRIVATE
        "$<$<CONFIG:Debug>:"
            "_DEBUG"
        ">"
        "_WIN32_WINNT=0x0600;"
        "_WIN32;"
        "WIN32;"
        "_SCL_SECURE_NO_WARNINGS;"
        "_CRT_SECURE_NO_WARNINGS;"
        "_LIB;"
        "UNICODE;"
        "_UNICODE"
    )
endif()

################################################################################
# Compile and link options
################################################################################
if(MSVC)
    if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "Any CPU")
        target_compile_options(${PROJECT_NAME} PRIVATE
            $<$<CONFIG:Debug>:
                /Od;
                /MDd
            >
            $<$<CONFIG:Release>:
                /O2;
                /Oi;
                /MD;
                /Gy
            >
            /std:c++17;
            /W3;
            /WX;
            ${DEFAULT_CXX_DEBUG_INFORMATION_FORMAT};
            ${DEFAULT_CXX_EXCEPTION_HANDLING};
            /Y-
        )
    elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "ARM")
        target_compile_options(${PROJECT_NAME} PRIVATE
            $<$<CONFIG:Debug>:
                /Od;
                /MDd
            >
            $<$<CONFIG:Release>:
                /O2;
                /Oi;
                /MD;
                /Gy
            >
            /W3;
            /WX;
            ${DEFAULT_CXX_DEBUG_INFORMATION_FORMAT};
            ${DEFAULT_CXX_EXCEPTION_HANDLING};
            /Y-
        )
    elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
        target_compile_options(${PROJECT_NAME} PRIVATE
            $<$<CONFIG:Debug>:
                /Od;
                /MDd
            >
            $<$<CONFIG:Release>:
                /O2;
                /Oi;
                /MD;
                /Gy
            >
            /std:c++17;
            /W3;
            /WX;
            ${DEFAULT_CXX_DEBUG_INFORMATION_FORMAT};
            ${DEFAULT_CXX_EXCEPTION_HANDLING};
            /Y-
        )
    elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
        target_compile_options(${PROJECT_NAME} PRIVATE
            $<$<CONFIG:Debug>:
                /Od;
                /MDd
            >
            $<$<CONFIG:Release>:
                /O2;
                /Oi;
                /MD;
                /Gy
            >
            /std:c++17;
            /W3;
            /WX;
            ${DEFAULT_CXX_DEBUG_INFORMATION_FORMAT};
            ${DEFAULT_CXX_EXCEPTION_HANDLING};
            /Y-
        )
    endif()
    if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "Any CPU")
        target_link_options(${PROJECT_NAME} PRIVATE
            $<$<CONFIG:Release>:
                /OPT:REF;
                /OPT:ICF
            >
            /SUBSYSTEM:CONSOLE
        )
    elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "ARM")
        target_link_options(${PROJECT_NAME} PRIVATE
            $<$<CONFIG:Release>:
                /OPT:REF;
                /OPT:ICF
            >
            /SUBSYSTEM:CONSOLE
        )
    elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
        target_link_options(${PROJECT_NAME} PRIVATE
            $<$<CONFIG:Release>:
                /OPT:REF;
                /OPT:ICF
            >
            /SUBSYSTEM:CONSOLE
        )
    elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
        target_link_options(${PROJECT_NAME} PRIVATE
            $<$<CONFIG:Release>:
                /OPT:REF;
                /OPT:ICF
            >
            /SUBSYSTEM:CONSOLE
        )
    endif()
endif()

################################################################################
# Dependencies
################################################################################
if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "Any CPU")
    target_link_directories(${PROJECT_NAME} PUBLIC
        "$ENV{BOOST_ROOT}/stage/lib"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "ARM")
    target_link_directories(${PROJECT_NAME} PUBLIC
        "$ENV{BOOST_ROOT}/stage/lib"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
    target_link_directories(${PROJECT_NAME} PUBLIC
        "$ENV{BOOST_ROOT}/stage/lib"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
    target_link_directories(${PROJECT_NAME} PUBLIC
        "$ENV{BOOST_ROOT}/stage/lib"
    )
endif()

