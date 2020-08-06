project(AirLib CXX)

################################################################################
# Source groups
################################################################################
set(Header_Files
    "include/api/ApiProvider.hpp"
    "include/api/ApiServerBase.hpp"
    "include/api/RpcLibAdapatorsBase.hpp"
    "include/api/RpcLibClientBase.hpp"
    "include/api/RpcLibServerBase.hpp"
    "include/api/VehicleApiBase.hpp"
    "include/api/VehicleConnectorBase.hpp"
    "include/api/VehicleSimApiBase.hpp"
    "include/api/WorldApiBase.hpp"
    "include/api/WorldSimApiBase.hpp"
    "include/common/AirSimSettings.hpp"
    "include/common/CancelToken.hpp"
    "include/common/ClockBase.hpp"
    "include/common/ClockFactory.hpp"
    "include/common/Common.hpp"
    "include/common/common_utils/AsyncTasker.hpp"
    "include/common/common_utils/bitmap_image.hpp"
    "include/common/common_utils/ColorUtils.hpp"
    "include/common/common_utils/ctpl_stl.h"
    "include/common/common_utils/EnumFlags.hpp"
    "include/common/common_utils/ExceptionUtils.hpp"
    "include/common/common_utils/FileSystem.hpp"
    "include/common/common_utils/json.hpp"
    "include/common/common_utils/MedianFilter.hpp"
    "include/common/common_utils/MinWinDefines.hpp"
    "include/common/common_utils/OnlineStats.hpp"
    "include/common/common_utils/optional.hpp"
    "include/common/common_utils/prettyprint.hpp"
    "include/common/common_utils/ProsumerQueue.hpp"
    "include/common/common_utils/RandomGenerator.hpp"
    "include/common/common_utils/ScheduledExecutor.hpp"
    "include/common/common_utils/Signal.hpp"
    "include/common/common_utils/sincos.hpp"
    "include/common/common_utils/SmoothingFilter.hpp"
    "include/common/common_utils/StrictMode.hpp"
    "include/common/common_utils/Timer.hpp"
    "include/common/common_utils/type_utils.hpp"
    "include/common/common_utils/UniqueValueMap.hpp"
    "include/common/common_utils/Utils.hpp"
    "include/common/common_utils/WindowsApisCommonPost.hpp"
    "include/common/common_utils/WindowsApisCommonPre.hpp"
    "include/common/CommonStructs.hpp"
    "include/common/DelayLine.hpp"
    "include/common/EarthCelestial.hpp"
    "include/common/EarthUtils.hpp"
    "include/common/FirstOrderFilter.hpp"
    "include/common/FrequencyLimiter.hpp"
    "include/common/GaussianMarkov.hpp"
    "include/common/GeodeticConverter.hpp"
    "include/common/ImageCaptureBase.hpp"
    "include/common/LogFileWriter.hpp"
    "include/common/PidController.hpp"
    "include/common/ScalableClock.hpp"
    "include/common/Settings.hpp"
    "include/common/StateReporter.hpp"
    "include/common/StateReporterWrapper.hpp"
    "include/common/SteppableClock.hpp"
    "include/common/UpdatableContainer.hpp"
    "include/common/UpdatableObject.hpp"
    "include/common/VectorMath.hpp"
    "include/common/Waiter.hpp"
    "include/common/WorkerThread.hpp"
    "include/physics/DebugPhysicsBody.hpp"
    "include/physics/Environment.hpp"
    "include/physics/FastPhysicsEngine.hpp"
    "include/physics/Kinematics.hpp"
    "include/physics/PhysicsBody.hpp"
    "include/physics/PhysicsBodyVertex.hpp"
    "include/physics/PhysicsBodyWorld.hpp"
    "include/physics/PhysicsEngineBase.hpp"
    "include/physics/PhysicsWorld.hpp"
    "include/physics/World.hpp"
    "include/safety/CubeGeoFence.hpp"
    "include/safety/IGeoFence.hpp"
    "include/safety/ObstacleMap.hpp"
    "include/safety/SafetyEval.hpp"
    "include/safety/SphereGeoFence.hpp"
    "include/sensors/barometer/BarometerBase.hpp"
    "include/sensors/barometer/BarometerSimple.hpp"
    "include/sensors/barometer/BarometerSimpleParams.hpp"
    "include/sensors/gps/GpsBase.hpp"
    "include/sensors/gps/GpsSimple.hpp"
    "include/sensors/gps/GpsSimpleParams.hpp"
    "include/sensors/imu/ImuBase.hpp"
    "include/sensors/imu/ImuSimple.hpp"
    "include/sensors/imu/ImuSimpleParams.hpp"
    "include/sensors/magnetometer/MagnetometerBase.hpp"
    "include/sensors/magnetometer/MagnetometerSimple.hpp"
    "include/sensors/magnetometer/MagnetometerSimpleParams.hpp"
    "include/sensors/SensorBase.hpp"
    "include/sensors/SensorCollection.hpp"
    "include/sensors/SensorFactory.hpp"
    "include/vehicles/car/api/CarApiBase.hpp"
    "include/vehicles/car/api/CarRpcLibAdapators.hpp"
    "include/vehicles/car/api/CarRpcLibClient.hpp"
    "include/vehicles/car/api/CarRpcLibServer.hpp"
    "include/vehicles/multirotor/api/MultirotorApiBase.hpp"
    "include/vehicles/multirotor/api/MultirotorCommon.hpp"
    "include/vehicles/multirotor/api/MultirotorRpcLibAdapators.hpp"
    "include/vehicles/multirotor/api/MultirotorRpcLibClient.hpp"
    "include/vehicles/multirotor/api/MultirotorRpcLibServer.hpp"
    "include/vehicles/multirotor/firmwares/mavlink/ArduCopterSoloApi.hpp"
    "include/vehicles/multirotor/firmwares/mavlink/ArduCopterSoloParams.hpp"
    "include/vehicles/multirotor/firmwares/mavlink/MavLinkMultirotorApi.hpp"
    "include/vehicles/multirotor/firmwares/mavlink/Px4MultiRotorParams.hpp"
    "include/vehicles/multirotor/firmwares/simple_flight/AirSimSimpleFlightBoard.hpp"
    "include/vehicles/multirotor/firmwares/simple_flight/AirSimSimpleFlightCommLink.hpp"
    "include/vehicles/multirotor/firmwares/simple_flight/AirSimSimpleFlightCommon.hpp"
    "include/vehicles/multirotor/firmwares/simple_flight/AirSimSimpleFlightEstimator.hpp"
    "include/vehicles/multirotor/firmwares/simple_flight/firmware/AdaptiveController.hpp"
    "include/vehicles/multirotor/firmwares/simple_flight/firmware/AngleLevelController.hpp"
    "include/vehicles/multirotor/firmwares/simple_flight/firmware/AngleRateController.hpp"
    "include/vehicles/multirotor/firmwares/simple_flight/firmware/CascadeController.hpp"
    "include/vehicles/multirotor/firmwares/simple_flight/firmware/ConstantOutputController.hpp"
    "include/vehicles/multirotor/firmwares/simple_flight/firmware/Firmware.hpp"
    "include/vehicles/multirotor/firmwares/simple_flight/firmware/interfaces/CommonStructs.hpp"
    "include/vehicles/multirotor/firmwares/simple_flight/firmware/interfaces/IAxisController.hpp"
    "include/vehicles/multirotor/firmwares/simple_flight/firmware/interfaces/IBoard.hpp"
    "include/vehicles/multirotor/firmwares/simple_flight/firmware/interfaces/IBoardClock.hpp"
    "include/vehicles/multirotor/firmwares/simple_flight/firmware/interfaces/IBoardInputPins.hpp"
    "include/vehicles/multirotor/firmwares/simple_flight/firmware/interfaces/IBoardOutputPins.hpp"
    "include/vehicles/multirotor/firmwares/simple_flight/firmware/interfaces/IBoardSensors.hpp"
    "include/vehicles/multirotor/firmwares/simple_flight/firmware/interfaces/ICommLink.hpp"
    "include/vehicles/multirotor/firmwares/simple_flight/firmware/interfaces/IController.hpp"
    "include/vehicles/multirotor/firmwares/simple_flight/firmware/interfaces/IFirmware.hpp"
    "include/vehicles/multirotor/firmwares/simple_flight/firmware/interfaces/IGoal.hpp"
    "include/vehicles/multirotor/firmwares/simple_flight/firmware/interfaces/IOffboardApi.hpp"
    "include/vehicles/multirotor/firmwares/simple_flight/firmware/interfaces/IPidIntegrator.hpp"
    "include/vehicles/multirotor/firmwares/simple_flight/firmware/interfaces/IStateEstimator.hpp"
    "include/vehicles/multirotor/firmwares/simple_flight/firmware/interfaces/IUpdatable.hpp"
    "include/vehicles/multirotor/firmwares/simple_flight/firmware/Mixer.hpp"
    "include/vehicles/multirotor/firmwares/simple_flight/firmware/OffboardApi.hpp"
    "include/vehicles/multirotor/firmwares/simple_flight/firmware/Params.hpp"
    "include/vehicles/multirotor/firmwares/simple_flight/firmware/PassthroughController.hpp"
    "include/vehicles/multirotor/firmwares/simple_flight/firmware/PidController.hpp"
    "include/vehicles/multirotor/firmwares/simple_flight/firmware/PositionController.hpp"
    "include/vehicles/multirotor/firmwares/simple_flight/firmware/RemoteControl.hpp"
    "include/vehicles/multirotor/firmwares/simple_flight/firmware/RungKuttaPidIntegrator.hpp"
    "include/vehicles/multirotor/firmwares/simple_flight/firmware/StdPidIntegrator.hpp"
    "include/vehicles/multirotor/firmwares/simple_flight/firmware/VelocityController.hpp"
    "include/vehicles/multirotor/firmwares/simple_flight/SimpleFlightApi.hpp"
    "include/vehicles/multirotor/firmwares/simple_flight/SimpleFlightQuadXParams.hpp"
    "include/vehicles/multirotor/MultiRotorParams.hpp"
    "include/vehicles/multirotor/MultiRotorParamsFactory.hpp"
    "include/vehicles/multirotor/MultiRotorPhysicsBody.hpp"
    "include/vehicles/multirotor/RotorActuator.hpp"
    "include/vehicles/multirotor/RotorParams.hpp"
)
source_group("Header Files" FILES ${Header_Files})

set(Source_Files
    "src/api/RpcLibClientBase.cpp"
    "src/api/RpcLibServerBase.cpp"
    "src/common/common_utils/FileSystem.cpp"
    "src/safety/ObstacleMap.cpp"
    "src/safety/SafetyEval.cpp"
    "src/vehicles/car/api/CarRpcLibClient.cpp"
    "src/vehicles/car/api/CarRpcLibServer.cpp"
    "src/vehicles/multirotor/api/MultirotorApiBase.cpp"
    "src/vehicles/multirotor/api/MultirotorRpcLibClient.cpp"
    "src/vehicles/multirotor/api/MultirotorRpcLibServer.cpp"
)
source_group("Source Files" FILES ${Source_Files})

set(ALL_FILES
    ${Header_Files}
    ${Source_Files}
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

set(ROOT_NAMESPACE AirLib)

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
        "${CMAKE_CURRENT_SOURCE_DIR}/include;"
        "${CMAKE_CURRENT_SOURCE_DIR}/deps/eigen3;"
        "${CMAKE_CURRENT_SOURCE_DIR}/deps/rpclib/include;"
        "${CMAKE_CURRENT_SOURCE_DIR}/../MavLinkCom/include"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "ARM")
    target_include_directories(${PROJECT_NAME} PUBLIC
        "${CMAKE_CURRENT_SOURCE_DIR}/include;"
        "${CMAKE_CURRENT_SOURCE_DIR}/deps/eigen3;"
        "${CMAKE_CURRENT_SOURCE_DIR}/deps/rpclib/include;"
        "${CMAKE_CURRENT_SOURCE_DIR}/../MavLinkCom/include"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
    target_include_directories(${PROJECT_NAME} PUBLIC
        "${CMAKE_CURRENT_SOURCE_DIR}/include;"
        "${CMAKE_CURRENT_SOURCE_DIR}/deps/eigen3;"
        "${CMAKE_CURRENT_SOURCE_DIR}/deps/rpclib/include;"
        "${CMAKE_CURRENT_SOURCE_DIR}/../MavLinkCom/include"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
    target_include_directories(${PROJECT_NAME} PUBLIC
        "${CMAKE_CURRENT_SOURCE_DIR}/include;"
        "${CMAKE_CURRENT_SOURCE_DIR}/deps/eigen3;"
        "${CMAKE_CURRENT_SOURCE_DIR}/deps/rpclib/include;"
        "${CMAKE_CURRENT_SOURCE_DIR}/../MavLinkCom/include"
    )
endif()

################################################################################
# Compile definitions
################################################################################
if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "Any CPU")
    target_compile_definitions(${PROJECT_NAME} PRIVATE
        "$<$<CONFIG:Debug>:"
            "_DEBUG;"
            "_CONSOLE"
        ">"
        "$<$<CONFIG:Release>:"
            "NDEBUG;"
            "_LIB"
        ">"
        "WIN32;"
        "UNICODE;"
        "_UNICODE"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "ARM")
    target_compile_definitions(${PROJECT_NAME} PRIVATE
        "$<$<CONFIG:Debug>:"
            "_DEBUG;"
            "_CONSOLE"
        ">"
        "$<$<CONFIG:Release>:"
            "NDEBUG;"
            "_LIB"
        ">"
        "WIN32;"
        "UNICODE;"
        "_UNICODE"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
    target_compile_definitions(${PROJECT_NAME} PRIVATE
        "$<$<CONFIG:Debug>:"
            "_DEBUG"
        ">"
        "$<$<CONFIG:Release>:"
            "NDEBUG"
        ">"
        "_SCL_SECURE_NO_WARNINGS;"
        "_CRT_SECURE_NO_WARNINGS;"
        "_LIB;"
        "UNICODE;"
        "_UNICODE"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
    target_compile_definitions(${PROJECT_NAME} PRIVATE
        "$<$<CONFIG:Debug>:"
            "_DEBUG;"
            "_CONSOLE"
        ">"
        "$<$<CONFIG:Release>:"
            "NDEBUG;"
            "_LIB"
        ">"
        "WIN32;"
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
                ${DEFAULT_CXX_DEBUG_RUNTIME_LIBRARY}
            >
            $<$<CONFIG:Release>:
                /O2;
                /Oi;
                ${DEFAULT_CXX_RUNTIME_LIBRARY};
                /Gy
            >
            /std:c++17;
            /W4;
            /WX;
            ${DEFAULT_CXX_DEBUG_INFORMATION_FORMAT};
            /w34263;
            /w34266;
            ${DEFAULT_CXX_EXCEPTION_HANDLING};
            /Y-
        )
    elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "ARM")
        target_compile_options(${PROJECT_NAME} PRIVATE
            $<$<CONFIG:Debug>:
                /Od;
                ${DEFAULT_CXX_DEBUG_RUNTIME_LIBRARY}
            >
            $<$<CONFIG:Release>:
                /O2;
                /Oi;
                ${DEFAULT_CXX_RUNTIME_LIBRARY};
                /Gy
            >
            /std:c++17;
            /W4;
            /WX;
            ${DEFAULT_CXX_DEBUG_INFORMATION_FORMAT};
            /w34263;
            /w34266;
            ${DEFAULT_CXX_EXCEPTION_HANDLING};
            /Y-
        )
    elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
        target_compile_options(${PROJECT_NAME} PRIVATE
            $<$<CONFIG:Debug>:
                /Od;
                ${DEFAULT_CXX_DEBUG_RUNTIME_LIBRARY};
                /wd4100;
                /wd4505;
                /wd4820;
                /wd4464;
                /wd4514;
                /wd4710;
                /wd4571
            >
            $<$<CONFIG:Release>:
                /O2;
                /Oi;
                ${DEFAULT_CXX_RUNTIME_LIBRARY};
                /Gy
            >
            /std:c++17;
            /W4;
            /WX;
            ${DEFAULT_CXX_DEBUG_INFORMATION_FORMAT};
            /w34263;
            /w34266;
            ${DEFAULT_CXX_EXCEPTION_HANDLING};
            /Y-
        )
    elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
        target_compile_options(${PROJECT_NAME} PRIVATE
            $<$<CONFIG:Debug>:
                /Od;
                ${DEFAULT_CXX_DEBUG_RUNTIME_LIBRARY}
            >
            $<$<CONFIG:Release>:
                /O2;
                /Oi;
                ${DEFAULT_CXX_RUNTIME_LIBRARY};
                /Gy
            >
            /std:c++17;
            /W4;
            /WX;
            ${DEFAULT_CXX_DEBUG_INFORMATION_FORMAT};
            /w34263;
            /w34266;
            ${DEFAULT_CXX_EXCEPTION_HANDLING};
            /Y-
        )
    endif()
    if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "Any CPU")
        target_link_options(${PROJECT_NAME} PRIVATE
            $<$<CONFIG:Debug>:
                /SUBSYSTEM:CONSOLE
            >
            $<$<CONFIG:Release>:
                /SUBSYSTEM:WINDOWS;
                /OPT:REF;
                /OPT:ICF
            >
        )
    elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "ARM")
        target_link_options(${PROJECT_NAME} PRIVATE
            $<$<CONFIG:Debug>:
                /SUBSYSTEM:CONSOLE
            >
            $<$<CONFIG:Release>:
                /SUBSYSTEM:WINDOWS;
                /OPT:REF;
                /OPT:ICF
            >
        )
    elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
        target_link_options(${PROJECT_NAME} PRIVATE
            $<$<CONFIG:Release>:
                /OPT:REF;
                /OPT:ICF
            >
            /SUBSYSTEM:WINDOWS
        )
    elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
        target_link_options(${PROJECT_NAME} PRIVATE
            $<$<CONFIG:Debug>:
                /SUBSYSTEM:CONSOLE
            >
            $<$<CONFIG:Release>:
                /SUBSYSTEM:WINDOWS;
                /OPT:REF;
                /OPT:ICF
            >
        )
    endif()
endif()

################################################################################
# Dependencies
################################################################################
add_dependencies(${PROJECT_NAME}
    MavLinkCom
)

# Link with other targets.
target_link_libraries(${PROJECT_NAME} PUBLIC
    MavLinkCom
)

if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "Any CPU")
    set(ADDITIONAL_LIBRARY_DEPENDENCIES
        "rpc"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "ARM")
    set(ADDITIONAL_LIBRARY_DEPENDENCIES
        "rpc"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
    set(ADDITIONAL_LIBRARY_DEPENDENCIES
        "rpc"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
    set(ADDITIONAL_LIBRARY_DEPENDENCIES
        "rpc"
    )
endif()
target_link_libraries(${PROJECT_NAME} PUBLIC "${ADDITIONAL_LIBRARY_DEPENDENCIES}")

if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "Any CPU")
    target_link_directories(${PROJECT_NAME} PUBLIC
        "${CMAKE_CURRENT_SOURCE_DIR}/deps/rpclib/lib/${CMAKE_VS_PLATFORM_NAME}/$<CONFIG>"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "ARM")
    target_link_directories(${PROJECT_NAME} PUBLIC
        "${CMAKE_CURRENT_SOURCE_DIR}/deps/rpclib/lib/${CMAKE_VS_PLATFORM_NAME}/$<CONFIG>"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
    target_link_directories(${PROJECT_NAME} PUBLIC
        "${CMAKE_CURRENT_SOURCE_DIR}/deps/rpclib/lib/${CMAKE_VS_PLATFORM_NAME}/$<CONFIG>"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
    target_link_directories(${PROJECT_NAME} PUBLIC
        "${CMAKE_CURRENT_SOURCE_DIR}/deps/rpclib/lib/${CMAKE_VS_PLATFORM_NAME}/$<CONFIG>"
    )
endif()

