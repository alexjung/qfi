cmake_minimum_required(VERSION 3.1.0)
project(qfi)

option(BuildQfiExample "Option to enable/disable building of example binary" ON)

set(CMAKE_BINARY_DIR ${CMAKE_BINARY_DIR})
set(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR})
set(LIBRARY_OUTPUT_PATH ${CMAKE_BINARY_DIR})
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

if(DEFINED ENV{CC})
    set(CMAKE_C_COMPILER $ENV{CC})
endif()

if(DEFINED ENV{CXX})
    set(CMAKE_CXX_COMPILER $ENV{CXX})
endif()

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -Wall")

set(PROJECT_SOURCE_DIR ${PROJECT_SOURCE_DIR}/src)


set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTORCC ON)

find_package(Qt5 COMPONENTS Widgets Svg REQUIRED)

set(QFI_SRCS
    ${PROJECT_SOURCE_DIR}/Adi.cpp
    ${PROJECT_SOURCE_DIR}/Alt.cpp
    ${PROJECT_SOURCE_DIR}/Asi.cpp
    ${PROJECT_SOURCE_DIR}/Hsi.cpp
    ${PROJECT_SOURCE_DIR}/Nav.cpp
    ${PROJECT_SOURCE_DIR}/Pfd.cpp
    ${PROJECT_SOURCE_DIR}/Tc.cpp
    ${PROJECT_SOURCE_DIR}/Vsi.cpp
    )

add_library(qfi STATIC ${QFI_SRCS} ${PROJECT_SOURCE_DIR}/qfi.qrc)
target_include_directories(qfi PRIVATE ${PROJECT_SOURCE_DIR})
target_link_libraries(qfi Qt5::Widgets Qt5::Svg)

if(BuildQfiExample)

    set(EXAMPLE_SRCS
        ${PROJECT_SOURCE_DIR}/example/LayoutSquare.cpp

        ${PROJECT_SOURCE_DIR}/example/MainWindow.ui
        ${PROJECT_SOURCE_DIR}/example/MainWindow.cpp
        ${PROJECT_SOURCE_DIR}/example/WidgetADI.ui
        ${PROJECT_SOURCE_DIR}/example/WidgetADI.cpp
        ${PROJECT_SOURCE_DIR}/example/WidgetALT.ui
        ${PROJECT_SOURCE_DIR}/example/WidgetALT.cpp
        ${PROJECT_SOURCE_DIR}/example/WidgetASI.ui
        ${PROJECT_SOURCE_DIR}/example/WidgetASI.cpp
        ${PROJECT_SOURCE_DIR}/example/WidgetHSI.ui
        ${PROJECT_SOURCE_DIR}/example/WidgetHSI.cpp
        ${PROJECT_SOURCE_DIR}/example/WidgetNAV.ui
        ${PROJECT_SOURCE_DIR}/example/WidgetNAV.cpp
        ${PROJECT_SOURCE_DIR}/example/WidgetPFD.ui
        ${PROJECT_SOURCE_DIR}/example/WidgetPFD.cpp
        ${PROJECT_SOURCE_DIR}/example/WidgetSix.ui
        ${PROJECT_SOURCE_DIR}/example/WidgetSix.cpp
        ${PROJECT_SOURCE_DIR}/example/WidgetTC.ui
        ${PROJECT_SOURCE_DIR}/example/WidgetTC.cpp
        ${PROJECT_SOURCE_DIR}/example/WidgetVSI.ui
        ${PROJECT_SOURCE_DIR}/example/WidgetVSI.cpp
        )

    add_executable(example ${PROJECT_SOURCE_DIR}/example/main.cpp ${EXAMPLE_SRCS})
    target_include_directories(example PRIVATE ${PROJECT_SOURCE_DIR} ${PROJECT_SOURCE_DIR}/example)
    target_link_libraries(example qfi)

endif()
