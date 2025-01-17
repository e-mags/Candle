# qt_add_plugin(qtscript_printsupport)
add_library(qtscript_printsupport MODULE)
file(GLOB generated_cpp 
../../generated_cpp/com_trolltech_qt_printsupport/*.cpp)

target_sources(qtscript_printsupport PRIVATE
    plugin.cpp plugin.h
    ${generated_cpp}
)
target_include_directories(qtscript_printsupport PRIVATE
    .
    include
    ../../generated_cpp/com_trolltech_qt_printsupport
)

target_link_libraries(qtscript_printsupport PRIVATE
    Qt::Core
    Qt::Gui
    Qt::PrintSupport
    Qt::Script
    Qt::Widgets
)

if(WIN32)
    target_compile_options(qtscript_printsupport PRIVATE
        "/GS"
        "/MP"
        "/Zi"
    )
endif()

install(TARGETS qtscript_printsupport
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    FRAMEWORK DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)
