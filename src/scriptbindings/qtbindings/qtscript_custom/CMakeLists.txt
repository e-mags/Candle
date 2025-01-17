cmake_minimum_required(VERSION 3.16)
project(qtscript_custom VERSION 1.0 LANGUAGES C CXX)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

# Set up AUTOMOC and some sensible defaults for runtime execution
# When using Qt 6.3, you can replace the code block below with
# qt_standard_project_setup()
set(CMAKE_AUTOMOC ON)
include(GNUInstallDirs)

find_package(QT NAMES Qt5 Qt6 REQUIRED COMPONENTS Core)
find_package(Qt${QT_VERSION_MAJOR} REQUIRED COMPONENTS Gui Script Widgets)
file(GLOB generated_cpp 
../../generated_cpp/com_trolltech_qt_custom/*.cpp)

add_library(qtscript_custom MODULE)
target_sources(qtscript_custom PRIVATE
    plugin.cpp plugin.h
    ${generated_cpp}
)
target_include_directories(qtscript_custom PRIVATE
    .
    ../../../designerplugins/customwidgetsplugin
    include
    ../../generated_cpp/com_trolltech_qt_custom
)

target_link_libraries(qtscript_custom PRIVATE
    # Remove: L${CMAKE_CURRENT_SOURCE_DIR}/../../../designerplugins/customwidgetsplugin/release
    Qt::Core
    Qt::Gui
    Qt::Script
    Qt::Widgets
    customwidgets
)

if(WIN32)
    target_compile_options(qtscript_custom PRIVATE
        "/GS"
        "/MP"
        "/Zi"
    )
endif()

install(TARGETS qtscript_custom
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    FRAMEWORK DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)
