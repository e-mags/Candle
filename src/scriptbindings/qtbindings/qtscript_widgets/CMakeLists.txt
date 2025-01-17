# qt_add_plugin(qtscript_widgets)
add_library(qtscript_widgets MODULE)
file(GLOB generated_cpp 
../../generated_cpp/com_trolltech_qt_widgets/*.cpp)
target_sources(qtscript_widgets PRIVATE
    plugin.cpp plugin.h
    ${generated_cpp}
)
target_include_directories(qtscript_widgets PRIVATE
    .
    include
    ../../generated_cpp/com_trolltech_qt_widgets
)

target_link_libraries(qtscript_widgets PRIVATE
    Qt::Core
    Qt::Gui
    Qt::Script
    Qt::Widgets
)

if(WIN32)
    target_compile_options(qtscript_widgets PRIVATE
        "/GS" "/MP" "/Zi"
    )
endif()

install(TARGETS qtscript_widgets
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    FRAMEWORK DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)
