cmake_minimum_required(VERSION 3.16)
# project(designerplugins VERSION 1.2 LANGUAGES C CXX)

# set(CMAKE_INCLUDE_CURRENT_DIR ON)

# # Set up AUTOMOC and some sensible defaults for runtime execution
# # When using Qt 6.3, you can replace the code block below with
# # qt_standard_project_setup()
# set(CMAKE_AUTOMOC ON)
# include(GNUInstallDirs)

# find_package(QT NAMES Qt5 REQUIRED COMPONENTS Core)
# find_package(Qt${QT_VERSION_MAJOR} REQUIRED COMPONENTS Gui Multimedia MultimediaWidgets UiPlugin Widgets)


add_subdirectory(cameraplugin)
add_subdirectory(customwidgetsplugin)
