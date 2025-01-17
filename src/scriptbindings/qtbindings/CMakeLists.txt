cmake_minimum_required(VERSION 3.16)
project(qtbindings VERSION 1.0 LANGUAGES C CXX)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

# Set up AUTOMOC and some sensible defaults for runtime execution
# When using Qt 6.3, you can replace the code block below with
# qt_standard_project_setup()
set(CMAKE_AUTOMOC ON)
include(GNUInstallDirs)

find_package(QT NAMES Qt5 REQUIRED COMPONENTS Core)
find_package(Qt${QT_VERSION_MAJOR} REQUIRED COMPONENTS Concurrent Gui Multimedia Network OpenGL PrintSupport Script Sql UiTools Widgets Xml)


add_subdirectory(qtscript_core)
add_subdirectory(qtscript_gui)
add_subdirectory(qtscript_widgets)
add_subdirectory(qtscript_printsupport)
add_subdirectory(qtscript_multimedia)
add_subdirectory(qtscript_network)
add_subdirectory(qtscript_opengl)
add_subdirectory(qtscript_sql)
add_subdirectory(qtscript_xml)
add_subdirectory(qtscript_uitools)
add_subdirectory(qtscript_custom)
