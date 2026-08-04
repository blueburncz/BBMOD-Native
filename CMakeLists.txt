cmake_minimum_required(VERSION 3.23)

project(BBMOD_Native LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

if(APPLE)
    set(CMAKE_OSX_ARCHITECTURES "x86_64;arm64" CACHE STRING "" FORCE)
endif()

set(ASSIMP_BUILD_TESTS OFF CACHE BOOL "" FORCE)
set(ASSIMP_BUILD_ASSIMP_TOOLS OFF CACHE BOOL "" FORCE)
set(ASSIMP_INSTALL OFF CACHE BOOL "" FORCE)

set(BUILD_SHARED_LIBS ON CACHE BOOL "" FORCE)
add_subdirectory(external/assimp)

add_library(BBMOD_CORE STATIC
    src/BBMOD/Animation.cpp
    src/BBMOD/Bone.cpp
    src/BBMOD/Importer.cpp
    src/BBMOD/Mesh.cpp
    src/BBMOD/Model.cpp
    src/BBMOD/Node.cpp
    src/BBMOD/VertexFormat.cpp
)

target_include_directories(BBMOD_CORE
    PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include
)

target_link_libraries(BBMOD_CORE
    PUBLIC assimp
)