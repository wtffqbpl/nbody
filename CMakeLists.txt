cmake_minimum_required(VERSION 3.20)
project(galaxy-nbody)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(CMAKE_INSTALL_BINDIR ${CMAKE_SOURCE_DIR}/bin)
set(CMAKE_INSTALL_LIBDIR ${CMAKE_SOURCE_DIR}/lib)

find_package(OpenGL REQUIRED)
include_directories(${OPENGL_INCLUDE_DIRS})

find_package(GLEW REQUIRED)
include_directories(${GLEW_INCLUDE_DIRS})

set(nbody_srcs
        src/nbody.cpp
        src/render_particles.cpp
        )

set(target nbody)
add_executable(${target} ${nbody_srcs})
target_compile_features(${target} PUBLIC cxx_std_20)
install(TARGETS ${target})

target_include_directories(${target} PUBLIC src inc)

target_link_libraries(${target} PRIVATE "-framework GLUT")
target_link_libraries(${target} PRIVATE "-framework OpenGL")