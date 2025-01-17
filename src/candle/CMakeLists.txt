cmake_minimum_required(VERSION 3.16)

# project(Candle VERSION 1.2.0 LANGUAGES CXX)


set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_AUTOUIC ON)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

find_package(Qt5 COMPONENTS Widgets Gui OpenGL SerialPort UiTools Script WinExtras REQUIRED)

add_executable(Candle
drawers/gcodedrawer.cpp drawers/gcodedrawer.h
drawers/heightmapborderdrawer.cpp drawers/heightmapborderdrawer.h
drawers/heightmapgriddrawer.cpp drawers/heightmapgriddrawer.h
drawers/heightmapinterpolationdrawer.cpp drawers/heightmapinterpolationdrawer.h
drawers/machineboundsdrawer.cpp drawers/machineboundsdrawer.h
drawers/origindrawer.cpp drawers/origindrawer.h
drawers/selectiondrawer.cpp drawers/selectiondrawer.h
drawers/shaderdrawable.cpp drawers/shaderdrawable.h
drawers/tooldrawer.cpp drawers/tooldrawer.h
frmabout.cpp frmabout.h frmabout.ui
frmmain.cpp frmmain.h frmmain.ui
frmsettings.cpp frmsettings.h frmsettings.ui
main.cpp
parser/arcproperties.cpp parser/arcproperties.h
parser/gcodeparser.cpp parser/gcodeparser.h
parser/gcodepreprocessorutils.cpp parser/gcodepreprocessorutils.h
parser/gcodeviewparse.cpp parser/gcodeviewparse.h
parser/linesegment.cpp parser/linesegment.h
parser/pointsegment.cpp parser/pointsegment.h
scriptfunctions.cpp scriptfunctions.h
scriptvars.cpp scriptvars.h
tables/gcodetablemodel.cpp tables/gcodetablemodel.h
tables/heightmaptablemodel.cpp tables/heightmaptablemodel.h
utils/interpolation.h
utils/util.h
widgets/combobox.cpp widgets/combobox.h
widgets/comboboxkey.cpp widgets/comboboxkey.h
widgets/dropwidget.cpp widgets/dropwidget.h
widgets/glwidget.cpp widgets/glwidget.h
shaders.qrc images.qrc
)

target_include_directories(Candle PRIVATE
    ../designerplugins/customwidgetsplugin
)

target_compile_definitions(Candle PRIVATE
    _USE_MATH_DEFINES
    sNan=65536
)

target_link_directories(Candle PRIVATE
    ../designerplugins/customwidgetsplugin
)

target_link_libraries(Candle 
    Qt::Widgets
    Qt::Core
    Qt::Gui
    Qt::OpenGL
    Qt::SerialPort
    Qt::UiTools
    Qt::Script
    Qt::WinExtras
    customwidgets
)


if(WIN32)
    target_compile_definitions(Candle PRIVATE
        WINDOWS
    )

endif()

install(TARGETS Candle
    BUNDLE DESTINATION .
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)