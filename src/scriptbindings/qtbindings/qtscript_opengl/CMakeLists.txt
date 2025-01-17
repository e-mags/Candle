cmake_minimum_required(VERSION 3.16)
project(qtscript_opengl VERSION 1.0 LANGUAGES C CXX)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

# Set up AUTOMOC and some sensible defaults for runtime execution
# When using Qt 6.3, you can replace the code block below with
# qt_standard_project_setup()
set(CMAKE_AUTOMOC ON)
include(GNUInstallDirs)

find_package(QT NAMES Qt5 Qt6 REQUIRED COMPONENTS Core)
find_package(Qt${QT_VERSION_MAJOR} REQUIRED COMPONENTS Gui OpenGL Script)

file(GLOB generated_cpp 
../../generated_cpp/com_trolltech_qt_opengl/*.cpp)
# qt_add_plugin(qtscript_opengl)
add_library(qtscript_opengl MODULE)
target_sources(qtscript_opengl PRIVATE
    plugin.cpp plugin.h
    ${generated_cpp}
)
target_include_directories(qtscript_opengl PRIVATE
    .
    include
    ../../generated_cpp/com_trolltech_qt_opengl
)

target_link_libraries(qtscript_opengl PRIVATE
    Qt::Core
    Qt::Gui
    Qt::OpenGL
    Qt::Script
)

if(WIN32)
    target_compile_options(qtscript_opengl PRIVATE
        "/GS"
        "/MP"
        "/Zi"
    )
endif()

install(TARGETS qtscript_opengl
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    FRAMEWORK DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)
