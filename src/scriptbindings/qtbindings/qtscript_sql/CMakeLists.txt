# qt_add_plugin(qtscript_sql)
add_library(qtscript_sql MODULE)

file(GLOB generated_cpp 
../../generated_cpp/com_trolltech_qt_sql/*.cpp)
target_sources(qtscript_sql PRIVATE
    plugin.cpp plugin.h
    ${generated_cpp}
)
target_include_directories(qtscript_sql PRIVATE
    .
    include
    ../../generated_cpp/com_trolltech_qt_sql
)

target_link_libraries(qtscript_sql PRIVATE
    Qt::Core
    Qt::Script
    Qt::Sql
)

if(WIN32)
    target_compile_options(qtscript_sql PRIVATE
        "/GS"
        "/MP"
        "/Zi"
    )
endif()

install(TARGETS qtscript_sql
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    FRAMEWORK DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)
