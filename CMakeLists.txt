PROJECT(SurvivalGame-CreateYourWolf C)

CMAKE_MINIMUM_REQUIRED(VERSION 2.6.0)

SET(CMAKE_COLOR_MAKEFILE ON)
SET(CMAKE_VERBOSE_MAKEFILE ON)

OPTION(ENABLE_PROFILING "Enable profiling." ON)

SET(CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake" ${CMAKE_MODULE_PATH})

FIND_PACKAGE(Threads REQUIRED)
FIND_PACKAGE(Curses REQUIRED)

SET(CMAKE_C_FLAGS "-D_BSD_SOURCE -g -std=c99 -Wall -W -O2")

IF (ENABLE_PROFILING)
    # If linux add gprof profiler.
    IF (${CMAKE_SYSTEM_NAME} MATCHES "Linux")
	SET(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -pg")
	SET(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -pg")
    ENDIF()
ENDIF()

SET(LIBS ${CMAKE_THREAD_LIBS_INIT} ncurses)

INCLUDE_DIRECTORIES(include)

# Set the source file
SET(SNAKENCURSES_SRC src/utils.c
		     src/header.c
		     src/footer.c
		     src/control.c
		     src/animal.c
		     src/main.c
		     src/attack_strategy.c
		     src/move_strategy.c)

ADD_EXECUTABLE(wolf ${SNAKENCURSES_SRC})

TARGET_LINK_LIBRARIES (wolf ${LIBS})
