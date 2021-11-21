cmake_minimum_required(VERSION 3.15)

add_library(${PROJECT_NAME}_wiringPi)
add_library(${PROJECT_NAME}::wiringPi ALIAS ${PROJECT_NAME}_wiringPi)
target_include_directories(${PROJECT_NAME}_wiringPi
    PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
    INTERFACE
        $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>
)

set_target_properties(${PROJECT_NAME}_wiringPi
    PROPERTIES
        OUTPUT_NAME wiringPi
        EXPORT_NAME wiringPi
        DEBUG_POSTFIX _d
        VERSION ${PROJECT_VERSION}
        SOVERSION ${PROJECT_VERSION_MAJOR}
        INSTALL_RPATH "${CMAKE_INSTALL_PREFIX}/${CMAKE_INSTALL_LIBDIR}"
)

target_sources(${PROJECT_NAME}_wiringPi
    PRIVATE
    # -- .h
        ads1115.h
        bmp180.h
        drcNet.h
        drcSerial.h
        ds18b20.h
        htu21d.h
        max5322.h
        max31855.h
        mcp23s08.h
        mcp23s17.h
        mcp23x08.h
        mcp23x0817.h
        mcp3002.h
        mcp3004.h
        mcp3422.h
        mcp4802.h
        mcp23008.h
        mcp23016.h
        mcp23016reg.h
        mcp23017.h
        pcf8574.h
        pcf8591.h
        pseudoPins.h
        rht03.h
        sn3218.h
        softPwm.h
        softServo.h
        softTone.h
        sr595.h
        wiringPi.h
        wiringPiI2C.h
        wiringPiSPI.h
        wiringSerial.h
        wiringShift.h
        wpiExtensions.h
    # -- .c
        ads1115.c
        bmp180.c
        drcNet.c
        drcSerial.c
        ds18b20.c
        htu21d.c
        max5322.c
        max31855.c
        mcp23s08.c
        mcp23s17.c
        mcp3002.c
        mcp3004.c
        mcp3422.c
        mcp4802.c
        mcp23008.c
        mcp23016.c
        mcp23017.c
        pcf8574.c
        pcf8591.c
        piHiPri.c
        piThread.c
        pseudoPins.c
        rht03.c
        sn3218.c
        softPwm.c
        softServo.c
        softTone.c
        sr595.c
        wiringPi.c
        wiringPiI2C.c
        wiringPiSPI.c
        wiringSerial.c
        wiringShift.c
        wpiExtensions.c
)


install(TARGETS ${PROJECT_NAME}_wiringPi
    EXPORT wiringPi
    PERMISSIONS
        OWNER_READ OWNER_WRITE OWNER_EXECUTE
        GROUP_READ GROUP_EXECUTE
        WORLD_READ WORLD_EXECUTE
)
install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/
    FILE_PERMISSIONS
        OWNER_READ OWNER_WRITE
        GROUP_READ WORLD_READ
    DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
    FILES_MATCHING PATTERN "*.h"
)
