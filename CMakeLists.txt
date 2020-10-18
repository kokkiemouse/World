cmake_minimum_required(VERSION 2.8)

set(PROJECT_NAME "WORLD")

project(${PROJECT_NAME})

FILE(GLOB SRCS "src/*.cpp" "src/*.c")

add_library(${PROJECT_NAME} SHARED ${SRCS})

target_include_directories(${PROJECT_NAME} PUBLIC 
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>)


install(TARGETS ${PROJECT_NAME}
    EXPORT ${PROJECT_NAME}-export
    LIBRARY        DESTINATION lib
    )
install(DIRECTORY  ${CMAKE_SOURCE_DIR}/include/world/ 
    DESTINATION include/world
    FILES_MATCHING PATTERN "*.h*")
install(EXPORT ${PROJECT_NAME}-export
    FILE ${PROJECT_NAME}-config.cmake
    DESTINATION share/cmake/${PROJECT_NAME}/
    )