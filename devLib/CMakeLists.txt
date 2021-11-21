cmake_minimum_required(VERSION 3.15)

add_library(${PROJECT_NAME}_wiringPiDev)
add_library(${PROJECT_NAME}::wiringPiDev ALIAS ${PROJECT_NAME}_wiringPiDev)
target_include_directories(${PROJECT_NAME}_wiringPiDev
    PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
    INTERFACE
        $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>
)
target_compile_definitions(${PROJECT_NAME}_wiringPiDev
    PRIVATE
        _GNU_SOURCE
)

set_target_properties(${PROJECT_NAME}_wiringPiDev
    PROPERTIES
        OUTPUT_NAME wiringPiDev
        EXPORT_NAME wiringPiDev
        DEBUG_POSTFIX _d
        VERSION ${PROJECT_VERSION}
        SOVERSION ${PROJECT_VERSION_MAJOR}
        INSTALL_RPATH "${CMAKE_INSTALL_PREFIX}/${CMAKE_INSTALL_LIBDIR}"
)

target_sources(${PROJECT_NAME}_wiringPiDev
    PRIVATE
    # -- .h
        ds1302.h
        font.h
        gertboard.h
        lcd.h
        lcd128x64.h
        maxdetect.h
        piFace.h
        piGlow.h
        piNes.h
        scrollPhat.h
        scrollPhatFont.h
    # -- .c
        ds1302.c
        gertboard.c
        lcd.c
        lcd128x64.c
        maxdetect.c
        piFace.c
        piGlow.c
        piNes.c
        scrollPhat.c
)


install(TARGETS ${PROJECT_NAME}_wiringPiDev
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
