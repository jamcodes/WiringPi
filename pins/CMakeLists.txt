cmake_minimum_required(VERSION 3.15)

if (WIRING_PI_MAKE_PINS OR "${CMAKE_SOURCE_DIR}/pins" STREQUAL "${CMAKE_CURRENT_SOURCE_DIR}")
    find_program(latexExec latex)
    find_program(dvipdfExec dvipdf)
    if (WIRING_PI_MAKE_PINS)
        set(_wiringPi_local_severity WARNING)
    else()
        set(_wiringPi_local_severity STATUS)
    endif()
    if (NOT latexExec)
        message(${_wiringPi_local_severity} "latex not found - can't generate pins.pdf")
    endif()
    if (NOT dvipdfExec)
        message(${_wiringPi_local_severity} "dvipdf not found - can't generate pins.pdf")
    endif()
    unset(_wiringPi_local_severity)

    add_custom_target(pins
        COMMAND make
        BYPRODUCTS pins.pdf
        DEPENDS pins.tex
        COMMENT "Generating pins.pdf"
        WORKING_DIRECTORY ${CMAKE_CURRENT_LIST_DIR}
    )
endif()
