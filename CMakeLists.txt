cmake_minimum_required(VERSION 3.16)

project(AuthoClicker VERSION 0.1 LANGUAGES CXX)

set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(QT NAMES Qt6 Qt5 REQUIRED COMPONENTS Widgets LinguistTools)
find_package(Qt${QT_VERSION_MAJOR} REQUIRED COMPONENTS Widgets LinguistTools)

set(SRC_DIR ${CMAKE_CURRENT_SOURCE_DIR}/Source)
set(RESOURCES_DIR ${SRC_DIR}/Resources)

set(TS_FILES
    ${RESOURCES_DIR}/AuthoClicker_ru_RU.ts
    ${RESOURCES_DIR}/AuthoClicker_en_US.ts
)

set(PROJECT_SOURCES
    ${SRC_DIR}/Application/main.cpp
    ${SRC_DIR}/Presentation/MainWindow.cpp
    ${SRC_DIR}/Presentation/MainWindow.hpp
    ${SRC_DIR}/Presentation/MainWindow.ui
    ${TS_FILES}
)

qt_add_executable(AuthoClicker
    MANUAL_FINALIZATION
    ${PROJECT_SOURCES}
)

qt_create_translation(QM_FILES ${SRC_DIR} ${TS_FILES})

target_link_libraries(AuthoClicker PRIVATE Qt${QT_VERSION_MAJOR}::Widgets)

set_target_properties(AuthoClicker PROPERTIES
    WIN32_EXECUTABLE TRUE
)

include(GNUInstallDirs)
install(TARGETS AuthoClicker
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)

if(QT_VERSION_MAJOR EQUAL 6)
    qt_finalize_executable(AuthoClicker)
endif()
