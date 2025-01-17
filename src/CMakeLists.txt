cmake_minimum_required(VERSION 3.13)
project(Candle)

# set(CMAKE_VERBOSE_MAKEFILE ON)

# instruct CMake to run moc automatically when needed
set(CMAKE_AUTOMOC ON)

# create code from a list of Qt designer ui files
set(CMAKE_AUTOUIC ON)
if(MINGW)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -W -msse3")
endif()

if(MSVC)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /W4 /arch:SSE4.2")
endif()
if(APPLE)
    add_compile_definitions(Q_OS_MAC)
endif()
add_compile_definitions(APP_VERSION="1.1.9-Qt6-mod")
add_compile_definitions(QT_NO_DEBUG)
add_compile_definitions(GLES)

find_package(Qt6 COMPONENTS Core Gui Widgets OpenGL OpenGLWidgets SerialPort Core5Compat REQUIRED)

add_compile_definitions(QT_DISABLE_DEPRECATED_UP_TO=0x050F00)

include_directories(${PROJECT_SOURCE_DIR})

file(GLOB SRC_FILES ${PROJECT_SOURCE_DIR}/*.cpp
                    ${PROJECT_SOURCE_DIR}/drawers/*.cpp
                    ${PROJECT_SOURCE_DIR}/parser/*.cpp
                    ${PROJECT_SOURCE_DIR}/widgets/*.cpp
                    ${PROJECT_SOURCE_DIR}/tables/*.cpp
                    )

qt6_add_resources(SHADER_RSC 
    ${PROJECT_SOURCE_DIR}/shaders.qrc
    ${PROJECT_SOURCE_DIR}/images.qrc
    ${PROJECT_SOURCE_DIR}/fonts.qrc
    )

if(APPLE)
    add_executable(Candle MACOSX_BUNDLE ${SRC_FILES} ${SHADER_RSC})
    set_target_properties(Candle PROPERTIES MACOSX_BUNDLE_INFO_PLIST ${PROJECT_SOURCE_DIR}/Info.plist)
else()
    add_executable(Candle ${SRC_FILES} ${SHADER_RSC})
endif()

set_target_properties(Candle PROPERTIES RUNTIME_OUTPUT_DIRECTORY "C:/Qt/6.8.1/msvc2022_64/lib")

target_link_libraries(Candle
    Qt6::Core
    Qt6::Widgets
    Qt6::OpenGL
    Qt6::Gui
    Qt6::SerialPort
    Qt6::Core5Compat
    Qt6::OpenGLWidgets
    )
