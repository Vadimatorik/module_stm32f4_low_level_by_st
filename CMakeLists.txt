CMAKE_MINIMUM_REQUIRED (VERSION 3.13.2)

project (MODULE_STM32F4_LOW_LEVEL_BY_ST)

if (NOT DEFINED HARDWARE_FLAGS)
    message(FATAL_ERROR "The value of the variable <<HARDWARE_FLAGS>> is not specified!")
endif ()

if (NOT DEFINED ${PROJECT_NAME}_COMP_FLAGS)
    message(FATAL_ERROR "The value of the variable <<${PROJECT_NAME}_COMP_FLAGS>> is not specified!")
endif ()

if (NOT DEFINED LIB_CFG_H_FILES_PATH)
    message(FATAL_ERROR "The value of the variable <<LIB_CFG_H_FILES_PATH>> is not specified!")
endif ()

include_directories(
    ${LIB_CFG_H_FILES_PATH}
    ${CMAKE_CURRENT_SOURCE_DIR}/cmsis/inc
    ${CMAKE_CURRENT_SOURCE_DIR}/cmsis/device/inc
    ${CMAKE_CURRENT_SOURCE_DIR}/hal/inc
    ${CMAKE_CURRENT_SOURCE_DIR}/hal/inc/legacy
)

file (GLOB ${PROJECT_NAME}_SRC_LIST "${CMAKE_CURRENT_SOURCE_DIR}/cmsis/device/src/*.c"
                                   "${CMAKE_CURRENT_SOURCE_DIR}/hal/src/*.c")

add_library(${PROJECT_NAME} STATIC ${${PROJECT_NAME}_SRC_LIST})

target_compile_options(${PROJECT_NAME} PRIVATE ${HARDWARE_FLAGS} ${${PROJECT_NAME}_COMP_FLAGS})