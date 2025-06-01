cmake_minimum_required(VERSION 3.31)
project(radon VERSION 1.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(Eigen3 3.3 REQUIRED NO_MODULE)

file(GLOB LIB_SOURCES
        "${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp"
)
list(FILTER LIB_SOURCES EXCLUDE REGEX ".*/main\\.cpp$")

add_library(radon STATIC
        ${LIB_SOURCES}
)

add_executable(radon_app
        "${CMAKE_CURRENT_SOURCE_DIR}/src/main.cpp"
)

target_include_directories(radon
        PUBLIC
        ${CMAKE_CURRENT_SOURCE_DIR}/include
)

target_link_libraries(radon_app
        PRIVATE
        radon
)

target_link_libraries(radon
        PRIVATE
        Eigen3::Eigen
)
