cmake_minimum_required(VERSION 3.1)
project(libigl_experiments)

### Conditionally compile certain modules depending on libraries found on the system
list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/../cmake)

### Compile libigl in header-only mode for Python bindings
option(LIBIGL_USE_STATIC_LIBRARY "Use LibIGL as static library" ON)

### Adding libIGL: choose the path to your local copy libIGL
if(NOT TARGET igl_common)
  include(libigl)
else()
  include(LibiglDownloadExternal)
endif()


### Output directories
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin")

#######################
if(NOT (LIBIGL_WITH_OPENGL AND LIBIGL_WITH_OPENGL_GLFW) )
  message(WARNING "Most tutorial executables depend on OpenGL and glfw. Use `cmake ../ -DLIBIGL_WITH_OPENGL=ON -DLIBIGL_WITH_OPENGL_GLFW=ON`")
  return()
endif()

add_subdirectory("CleanIntersection")