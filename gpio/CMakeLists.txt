cmake_minimum_required(VERSION 3.15)

add_executable(${PROJECT_NAME}_gpio)
target_include_directories(${PROJECT_NAME}_gpio
    PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
)
target_link_libraries(${PROJECT_NAME}_gpio
    PRIVATE
        ${PROJECT_NAME}_wiringPi
        ${PROJECT_NAME}_wiringPiDev
        Threads::Threads
        ${LibRt}
        ${LibM}
        ${LibCrypt}
)
set_target_properties(${PROJECT_NAME}_gpio
    PROPERTIES
        OUTPUT_NAME gpio
        EXPORT_NAME gpio
        INSTALL_RPATH ${CMAKE_INSTALL_PREFIX}/${CMAKE_INSTALL_LIBDIR}
)

target_sources(${PROJECT_NAME}_gpio
    PRIVATE
        gpio.c
        readall.c
)


install(TARGETS ${PROJECT_NAME}_gpio
    EXPORT wiringPi
    PERMISSIONS
        OWNER_READ OWNER_WRITE
        GROUP_READ GROUP_EXECUTE
        WORLD_READ WORLD_EXECUTE
        SETUID
        SETGID
    DESTINATION ${CMAKE_INSTALL_BINDIR}
)
