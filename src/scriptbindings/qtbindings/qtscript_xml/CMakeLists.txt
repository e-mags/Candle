# qt_add_plugin(qtscript_xml)
add_library(qtscript_xml MODULE)
file(GLOB generated_cpp 
../../generated_cpp/com_trolltech_qt_xml/*.cpp)
target_sources(qtscript_xml PRIVATE
    plugin.cpp plugin.h
    ${generated_cpp}
)
target_include_directories(qtscript_xml PRIVATE
    .
    include
    ../../generated_cpp/com_trolltech_qt_xml
)

target_link_libraries(qtscript_xml PRIVATE
    Qt::Core
    Qt::Script
    Qt::Xml
)

if(WIN32)
    target_compile_options(qtscript_xml PRIVATE
        "/GS"
        "/MP"
        "/Zi"
    )
endif()

install(TARGETS qtscript_xml
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    FRAMEWORK DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)
