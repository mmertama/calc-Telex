cmake_minimum_required (VERSION 3.14)

set(NAME calc)
project (${NAME})

set(CMAKE_CXX_STANDARD 17)

set(GEMPYRE_PATH $ENV{GEMPYRE_DIR})

include_directories(
    include
)

find_package (gempyre REQUIRED)
include(addResource)


add_executable(${PROJECT_NAME}
    src/computor.h
    src/main.cpp
    gui/${NAME}.html
    )

addResource(PROJECT ${PROJECT_NAME} TARGET include/${NAME}_resource.h SOURCES gui/${NAME}.html gui/${NAME}.css gui/${NAME}.png)

add_custom_command(
        OUTPUT include/${NAME}.html.h
        COMMAND python ${GEMPYRE_PATH}/scripts/genStringResource.py gui/${NAME}.html include/${NAME}.html.h WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
        DEPENDS gui/${NAME}.html
        )

target_link_libraries (${PROJECT_NAME} gempyre::gempyre)

