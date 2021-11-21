cmake_minimum_required(VERSION 3.15)

add_executable(${PROJECT_NAME}_wiringpid)
target_include_directories(${PROJECT_NAME}_wiringpid
    PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
)
target_link_libraries(${PROJECT_NAME}_wiringpid
    PRIVATE
        ${PROJECT_NAME}_wiringPi
        ${PROJECT_NAME}_wiringPiDev
        Threads::Threads
        ${LibRt}
        ${LibM}
        ${LibCrypt}
)
set_target_properties(${PROJECT_NAME}_wiringpid
    PROPERTIES
        OUTPUT_NAME wiringpid
        EXPORT_NAME wiringpid
    INSTALL_RPATH ${CMAKE_INSTALL_PREFIX}/${CMAKE_INSTALL_LIBDIR}
)

target_sources(${PROJECT_NAME}_wiringpid
    PRIVATE
    # -- .h
        daemonise.h
        drcNetCmd.h
        network.h
        runRemote.h
    # -- .c
        daemonise.c
        network.c
        runRemote.c
        wiringpid.c
)


install(TARGETS ${PROJECT_NAME}_wiringpid
    EXPORT wiringPi
    DESTINATION ${CMAKE_INSTALL_SBINDIR}
)
