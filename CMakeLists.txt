cmake_minimum_required(VERSION 3.13.0 FATAL_ERROR)

project(AirSim CXX)

################################################################################
# Set target arch type if empty. Visual studio solution generator provides it.
################################################################################
if(NOT CMAKE_VS_PLATFORM_NAME)
    set(CMAKE_VS_PLATFORM_NAME "x64")
endif()
message("${CMAKE_VS_PLATFORM_NAME} architecture in use")

if(NOT ("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "ARM"
     OR "${CMAKE_VS_PLATFORM_NAME}" STREQUAL "Any CPU"
     OR "${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64"
     OR "${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86"))
    message(FATAL_ERROR "${CMAKE_VS_PLATFORM_NAME} arch is not supported!")
endif()

################################################################################
# Global configuration types
################################################################################
set(CMAKE_CONFIGURATION_TYPES
    "Debug"
    "Release"
    CACHE STRING "" FORCE
)

################################################################################
# Global compiler options
################################################################################
if(MSVC)
    # remove default flags provided with CMake for MSVC
    set(CMAKE_CXX_FLAGS "")
    set(CMAKE_CXX_FLAGS_DEBUG "")
    set(CMAKE_CXX_FLAGS_RELEASE "")
endif()

################################################################################
# Global linker options
################################################################################
if(MSVC)
    # remove default flags provided with CMake for MSVC
    set(CMAKE_EXE_LINKER_FLAGS "")
    set(CMAKE_MODULE_LINKER_FLAGS "")
    set(CMAKE_SHARED_LINKER_FLAGS "")
    set(CMAKE_STATIC_LINKER_FLAGS "")
    set(CMAKE_EXE_LINKER_FLAGS_DEBUG "${CMAKE_EXE_LINKER_FLAGS}")
    set(CMAKE_MODULE_LINKER_FLAGS_DEBUG "${CMAKE_MODULE_LINKER_FLAGS}")
    set(CMAKE_SHARED_LINKER_FLAGS_DEBUG "${CMAKE_SHARED_LINKER_FLAGS}")
    set(CMAKE_STATIC_LINKER_FLAGS_DEBUG "${CMAKE_STATIC_LINKER_FLAGS}")
    set(CMAKE_EXE_LINKER_FLAGS_RELEASE "${CMAKE_EXE_LINKER_FLAGS}")
    set(CMAKE_MODULE_LINKER_FLAGS_RELEASE "${CMAKE_MODULE_LINKER_FLAGS}")
    set(CMAKE_SHARED_LINKER_FLAGS_RELEASE "${CMAKE_SHARED_LINKER_FLAGS}")
    set(CMAKE_STATIC_LINKER_FLAGS_RELEASE "${CMAKE_STATIC_LINKER_FLAGS}")
endif()

################################################################################
# Nuget packages function stub.
################################################################################
function(use_package TARGET PACKAGE VERSION)
    message(WARNING "No implementation of use_package. Create yours. "
                    "Package \"${PACKAGE}\" with version \"${VERSION}\" "
                    "for target \"${TARGET}\" is ignored!")
endfunction()

################################################################################
# Common utils
################################################################################
include(CMake/Utils.cmake)

################################################################################
# Additional Global Settings(add specific info there)
################################################################################
include(CMake/GlobalSettingsInclude.cmake OPTIONAL)

################################################################################
# Use solution folders feature
################################################################################
set_property(GLOBAL PROPERTY USE_FOLDERS ON)

################################################################################
# Sub-projects
################################################################################
add_subdirectory(AirLib)
add_subdirectory(AirLibUnitTests)
add_subdirectory(DroneServer)
add_subdirectory(DroneShell)
add_subdirectory(Examples)
add_subdirectory(HelloCar)
add_subdirectory(HelloDrone)
add_subdirectory(MavLinkCom)
add_subdirectory(MavLinkCom/MavLinkTest)
add_subdirectory(SGM/src/sgmstereo)
add_subdirectory(SGM/src/stereoPipeline)



























project(UnrealPluginFiles CXX)

################################################################################
# Source groups
################################################################################
set(Header_Files
    "Unreal/Plugins/AirSim/Source/AirBlueprintLib.h"
    "Unreal/Plugins/AirSim/Source/AirSim.h"
    "Unreal/Plugins/AirSim/Source/AirSimGameMode.h"
    "Unreal/Plugins/AirSim/Source/CameraDirector.h"
    "unreal/plugins/airsim/source/car/CarPawn.h"
    "unreal/plugins/airsim/source/car/CarWheelFront.h"
    "unreal/plugins/airsim/source/car/CarWheelRear.h"
    "unreal/plugins/airsim/source/car/SimModeCar.h"
    "Unreal/Plugins/AirSim/Source/ManualPoseController.h"
    "unreal/plugins/airsim/source/multirotor/FlyingPawn.h"
    "unreal/plugins/airsim/source/multirotor/MultiRotorConnector.h"
    "unreal/plugins/airsim/source/multirotor/SimModeWorldMultiRotor.h"
    "Unreal/Plugins/AirSim/Source/NedTransform.h"
    "Unreal/Plugins/AirSim/Source/PIPCamera.h"
    "Unreal/Plugins/AirSim/Source/Recording/RecordingFile.h"
    "Unreal/Plugins/AirSim/Source/Recording/RecordingThread.h"
    "Unreal/Plugins/AirSim/Source/RenderRequest.h"
    "Unreal/Plugins/AirSim/Source/SimHUD/SimHUD.h"
    "Unreal/Plugins/AirSim/Source/SimHUD/SimHUDWidget.h"
    "Unreal/Plugins/AirSim/Source/SimJoyStick/DirectInputJoystick.h"
    "Unreal/Plugins/AirSim/Source/SimJoyStick/SimJoyStick.h"
    "Unreal/Plugins/AirSim/Source/SimMode/SimModeBase.h"
    "Unreal/Plugins/AirSim/Source/SimMode/SimModeWorldBase.h"
    "unreal/plugins/airsim/source/VehicleCameraConnector.h"
    "unreal/plugins/airsim/source/VehiclePawnWrapper.h"
)
source_group("Header Files" FILES ${Header_Files})

set(Source_Files
    "Unreal/Plugins/AirSim/Source/AirBlueprintLib.cpp"
    "Unreal/Plugins/AirSim/Source/AirSim.Build.4.15.cs"
    "Unreal/Plugins/AirSim/Source/AirSim.Build.cs"
    "Unreal/Plugins/AirSim/Source/AirSim.cpp"
    "Unreal/Plugins/AirSim/Source/AirSimGameMode.cpp"
    "Unreal/Plugins/AirSim/Source/CameraDirector.cpp"
    "unreal/plugins/airsim/source/car/CarPawn.cpp"
    "unreal/plugins/airsim/source/car/CarWheelFront.cpp"
    "unreal/plugins/airsim/source/car/CarWheelRear.cpp"
    "unreal/plugins/airsim/source/car/SimModeCar.cpp"
    "Unreal/Plugins/AirSim/Source/ManualPoseController.cpp"
    "unreal/plugins/airsim/source/multirotor/FlyingPawn.cpp"
    "Unreal/Plugins/AirSim/Source/Multirotor/MultirotorSimApi.cpp"
    "Unreal/Plugins/AirSim/Source/Multirotor/MultirotorSimApi.h"
    "Unreal/Plugins/AirSim/Source/Multirotor/SimModeWorldMultirotor.cpp"
    "Unreal/Plugins/AirSim/Source/NedTransform.cpp"
    "Unreal/Plugins/AirSim/Source/PIPCamera.cpp"
    "Unreal/Plugins/AirSim/Source/Recording/RecordingFile.cpp"
    "Unreal/Plugins/AirSim/Source/Recording/RecordingThread.cpp"
    "Unreal/Plugins/AirSim/Source/RenderRequest.cpp"
    "Unreal/Plugins/AirSim/Source/SimHUD/SimHUD.cpp"
    "Unreal/Plugins/AirSim/Source/SimHUD/SimHUDWidget.cpp"
    "Unreal/Plugins/AirSim/Source/SimJoyStick/DirectInputJoyStick.cpp"
    "Unreal/Plugins/AirSim/Source/SimJoyStick/SimJoyStick.cpp"
    "Unreal/Plugins/AirSim/Source/SimMode/SimModeBase.cpp"
    "Unreal/Plugins/AirSim/Source/SimMode/SimModeWorldBase.cpp"
    "Unreal/Plugins/AirSim/Source/TextureShuffleActor.cpp"
    "Unreal/Plugins/AirSim/Source/UnrealImageCapture.cpp"
    "Unreal/Plugins/AirSim/Source/UnrealImageCapture.h"
    "Unreal/Plugins/AirSim/Source/UnrealSensors/UnrealDistanceSensor.cpp"
    "Unreal/Plugins/AirSim/Source/UnrealSensors/UnrealDistanceSensor.h"
    "Unreal/Plugins/AirSim/Source/UnrealSensors/UnrealLidarSensor.cpp"
    "Unreal/Plugins/AirSim/Source/UnrealSensors/UnrealLidarSensor.h"
    "Unreal/Plugins/AirSim/Source/UnrealSensors/UnrealSensorFactory.cpp"
    "Unreal/Plugins/AirSim/Source/UnrealSensors/UnrealSensorFactory.h"
    "unreal/plugins/airsim/source/VehicleCameraConnector.cpp"
    "Unreal/Plugins/AirSim/Source/VehicleSimApi.cpp"
    "Unreal/Plugins/AirSim/Source/VehicleSimApi.h"
    "Unreal/Plugins/AirSim/Source/Weather/WeatherLib.cpp"
    "Unreal/Plugins/AirSim/Source/Weather/WeatherLib.h"
    "Unreal/Plugins/AirSim/Source/WorldSimApi.cpp"
    "Unreal/Plugins/AirSim/Source/WorldSimApi.h"
)
source_group("Source Files" FILES ${Source_Files})

set(ALL_FILES
    ${Header_Files}
    ${Source_Files}
)

################################################################################
# Target
################################################################################
add_executable(${PROJECT_NAME} ${ALL_FILES})

use_props(${PROJECT_NAME} "${CMAKE_CONFIGURATION_TYPES}" "${DEFAULT_CXX_PROPS}")
set_target_properties(${PROJECT_NAME} PROPERTIES
    VS_GLOBAL_KEYWORD "MakeFileProj"
)
################################################################################
# Compile definitions
################################################################################

################################################################################
# Compile and link options
################################################################################
if(MSVC)
    if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "Any CPU")
        target_compile_options(${PROJECT_NAME} PRIVATE
            $<$<CONFIG:Debug>:
                ${DEFAULT_CXX_DEBUG_RUNTIME_LIBRARY}
            >
            $<$<CONFIG:Release>:
                ${DEFAULT_CXX_RUNTIME_LIBRARY}
            >
            ${DEFAULT_CXX_DEBUG_INFORMATION_FORMAT};
            ${DEFAULT_CXX_EXCEPTION_HANDLING}
        )
    elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "ARM")
        target_compile_options(${PROJECT_NAME} PRIVATE
            $<$<CONFIG:Debug>:
                ${DEFAULT_CXX_DEBUG_RUNTIME_LIBRARY}
            >
            $<$<CONFIG:Release>:
                ${DEFAULT_CXX_RUNTIME_LIBRARY}
            >
            ${DEFAULT_CXX_DEBUG_INFORMATION_FORMAT};
            ${DEFAULT_CXX_EXCEPTION_HANDLING}
        )
    elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
        target_compile_options(${PROJECT_NAME} PRIVATE
            $<$<CONFIG:Debug>:
                ${DEFAULT_CXX_DEBUG_RUNTIME_LIBRARY}
            >
            $<$<CONFIG:Release>:
                ${DEFAULT_CXX_RUNTIME_LIBRARY}
            >
            ${DEFAULT_CXX_DEBUG_INFORMATION_FORMAT};
            ${DEFAULT_CXX_EXCEPTION_HANDLING}
        )
    elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
        target_compile_options(${PROJECT_NAME} PRIVATE
            $<$<CONFIG:Debug>:
                ${DEFAULT_CXX_DEBUG_RUNTIME_LIBRARY}
            >
            $<$<CONFIG:Release>:
                ${DEFAULT_CXX_RUNTIME_LIBRARY}
            >
            ${DEFAULT_CXX_DEBUG_INFORMATION_FORMAT};
            ${DEFAULT_CXX_EXCEPTION_HANDLING}
        )
    endif()
    if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "Any CPU")
        target_link_options(${PROJECT_NAME} PRIVATE
            /DEBUG:FULL
        )
    elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "ARM")
        target_link_options(${PROJECT_NAME} PRIVATE
            /DEBUG:FULL
        )
    elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
        target_link_options(${PROJECT_NAME} PRIVATE
            /DEBUG:FULL
        )
    elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
        target_link_options(${PROJECT_NAME} PRIVATE
            /DEBUG:FULL
        )
    endif()
endif()

