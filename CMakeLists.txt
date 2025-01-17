cmake_minimum_required(VERSION 3.18.0)
# set(CMAKE_PREFIX_PATH "C:/Qt/5.15.2/msvc2019_64")

project(Candle)
add_subdirectory(src/designerplugins)
add_subdirectory(src/candle)
add_subdirectory(src/candleplugins)
add_subdirectory(src/scriptbindings)

