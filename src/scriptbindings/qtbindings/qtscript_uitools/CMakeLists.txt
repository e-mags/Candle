# qt_add_plugin(qtscript_uitools)
add_library(qtscript_uitools MODULE)
file(GLOB generated_cpp 
../../generated_cpp/com_trolltech_qt_uitools/*.cpp)
target_sources(qtscript_uitools PRIVATE
    plugin.cpp plugin.h
    ${generated_cpp}
)
target_include_directories(qtscript_uitools PRIVATE
    .
    include
    ../../generated_cpp/com_trolltech_qt_uitools
)

target_link_libraries(qtscript_uitools PRIVATE
    Qt::Core
    Qt::Gui
    Qt::Script
    Qt::UiTools
    Qt::Widgets
)

if(WIN32)
    target_compile_options(qtscript_uitools PRIVATE
        "/GS"
        "/MP"
        "/Zi"
    )
endif()

install(TARGETS qtscript_uitools
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    FRAMEWORK DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)
