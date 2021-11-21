cmake_minimum_required(VERSION 3.15)

file(STRINGS "VERSION" projectVersion)

project(wiringPi VERSION ${projectVersion} LANGUAGES C)


option(WIRING_PI_MAKE_PINS "Add target \"pins\" generating pins.pdf. Not called implicitly by the \"all\" target." OFF)

add_compile_options(
    -mcpu=cortex-a72
    -mfpu=neon-vfpv4
    -Wall
    -Wextra
    -Winline
    -pipe
)

set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_C_EXTENSIONS ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

find_package(Threads REQUIRED)
find_library(LibRt rt REQUIRED)
find_library(LibM m REQUIRED)
find_library(LibCrypt crypt REQUIRED)

include(GNUInstallDirs)


# file(RELATIVE_PATH relativeRpath
#     ${CMAKE_CURRENT_BINARY_DIR}/${CMAKE_INSTALL_BINDIR}
#     ${CMAKE_CURRENT_BINARY_DIR}/${CMAKE_INSTALL_LIBDIR}
# )
# set(CMAKE_INSTALL_RPATH $ORIGIN $ORIGIN/${relativeRpath})


add_subdirectory(devLib)
add_subdirectory(wiringPi)
add_subdirectory(wiringPiD)
add_subdirectory(gpio)
add_subdirectory(pins)

install(EXPORT wiringPi
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/wiringPi
    NAMESPACE wiringPi::
)

include(CMakePackageConfigHelpers)

configure_package_config_file(
    cmake/wiringPiConfig.cmake.in
    ${CMAKE_CURRENT_BINARY_DIR}/wiringPiConfig.cmake
    PATH_VARS CMAKE_INSTALL_INCLUDEDIR
    INSTALL_DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/wiringPi
)

write_basic_package_version_file(
    ${CMAKE_CURRENT_BINARY_DIR}/wiringPiConfigVersion.cmake
    VERSION ${PROJECT_VERSION}
    COMPATIBILITY SameMajorVersion
)

install(FILES
    ${CMAKE_CURRENT_BINARY_DIR}/wiringPiConfig.cmake
    ${CMAKE_CURRENT_BINARY_DIR}/wiringPiConfigVersion.cmake
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/wiringPi
)
