cmake_minimum_required(VERSION 3.12)

project(Firmware LANGUAGES CSharp CXX)

include(CTest)

enable_testing()
add_executable(test_basic Tests/test_basic.cpp)
set_target_properties(test_basic PROPERTIES LINKER_LANGUAGE CXX)
add_test(NAME BasicTest COMMAND test_basic)

set(CMAKE_DOTNET_TARGET_FRAMEWORK_VERSION "4.5.2")
set(CMAKE_CSharp_FLAGS "/langversion:7")

add_library(Firmware SHARED
	App.config
	src/FirmwareMain.cs
)

set_property(TARGET Firmware PROPERTY VS_DONET REFERENCES "Hardware/bin/Release/Hardware.dll")

#include(ExternalProject)

#ExternalProject_Add(Hardware
#	PREFIX ${CMAKE_BINARY_DIR}
#	GIT_REPOSITORY "https://github/com/dantmw/3DPrinterSIMHardware.git"
#	PATCH_COMMAND ""
#	BINARY_DIR ${CMAKE_BINARY_DIR}/Hardware
#	SOURCE_DIR ${CMAKE_BINARY_DIR}/Hardware
#	INSTALL_DIR ${CMAKE_BINARY_DIR}/Hardware
#	CONFIGURE_COMMAND ""
#	BUILD_COMMAND ""
#	INSTALL_COMMAND ""
#)


set_property(TARGET Firmware PROPERTY VS_DOTNET_REFERENCES "Hardware/bin/Release/Hardware.dll")

add_subdirectory(Tests)