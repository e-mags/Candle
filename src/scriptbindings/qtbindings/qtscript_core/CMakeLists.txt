add_library(qtscript_core MODULE)

file(GLOB generated_cpp 
../../generated_cpp/com_trolltech_qt_core/*.cpp)

target_sources(qtscript_core PRIVATE
    plugin.cpp plugin.h
    qtscriptconcurrent.h
    ${generated_cpp}
)

target_include_directories(qtscript_core PRIVATE
    .
    include
    ../../generated_cpp/com_trolltech_qt_core
)

target_link_libraries(qtscript_core PRIVATE
    Qt::Concurrent
    Qt::Core
    Qt::Gui
    Qt::Script
    Qt::Widgets
)

if(WIN32)
    target_compile_options(qtscript_core PRIVATE
        "/GS"
        "/MP"
        "/Zi"
    )
endif()

install(TARGETS qtscript_core
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    FRAMEWORK DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)
