cmake_minimum_required(VERSION 3.16)
project(qtscript_gui VERSION 1.0 LANGUAGES C CXX)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

# Set up AUTOMOC and some sensible defaults for runtime execution
# When using Qt 6.3, you can replace the code block below with
# qt_standard_project_setup()
set(CMAKE_AUTOMOC ON)
include(GNUInstallDirs)

find_package(QT NAMES Qt5 Qt6 REQUIRED COMPONENTS Core)
find_package(Qt${QT_VERSION_MAJOR} REQUIRED COMPONENTS Gui Script Widgets)
file(GLOB generated_cpp 
../../generated_cpp/com_trolltech_qt_gui/*.cpp)

# qt_add_plugin(qtscript_gui)
add_library(qtscript_gui MODULE)
target_sources(qtscript_gui PRIVATE
    plugin.cpp plugin.h
    ${generated_cpp}
)
target_include_directories(qtscript_gui PRIVATE
    .
    include
    ../../generated_cpp/com_trolltech_qt_gui
)

target_link_libraries(qtscript_gui PRIVATE
    Qt::Core
    Qt::Gui
    Qt::Script
    Qt::Widgets
)

if(WIN32)
    target_compile_options(qtscript_gui PRIVATE
        "/GS"
        "/MP"
        "/Zi"
    )
endif()

install(TARGETS qtscript_gui
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    FRAMEWORK DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)
