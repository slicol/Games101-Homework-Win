cmake_minimum_required(VERSION 3.10)

# Application source
set(APPLICATION_SOURCE
    rope.cpp
    application.cpp
    main.cpp
    getopt.c
    getopt_init.c
    ./../CGL/deps/glew/src/glew.c
    ./../CGL/src/osdfont.cpp
)

#-------------------------------------------------------------------------------
# Set include directories
#-------------------------------------------------------------------------------
include_directories(
  ${GLEW_INCLUDE_DIRS}
  ${GLFW_INCLUDE_DIRS}
  ${CGL_INCLUDE_DIRS}
  ${FREETYPE_INCLUDE_DIRS}
)

message("GLEW_INCLUDE_DIRS: ${GLEW_INCLUDE_DIRS}")
message("GLFW_INCLUDE_DIRS: ${GLFW_INCLUDE_DIRS}")
message("CGL_INCLUDE_DIRS: ${CGL_INCLUDE_DIRS}")
message("FREETYPE_INCLUDE_DIRS: ${FREETYPE_INCLUDE_DIRS}")

#-------------------------------------------------------------------------------
# Set link directories
#-------------------------------------------------------------------------------
link_directories(
  ${GLEW_LIBRARY_DIRS}
  ${GLFW_LIBRARY_DIRS}
  ${CGL_LIBRARY_DIRS}
  ${FREETYPE_LIBRARY_DIRS}
)

message("GLEW_LIBRARY_DIRS: ${GLEW_LIBRARY_DIRS}")
message("GLFW_LIBRARY_DIRS: ${GLFW_LIBRARY_DIRS}")
message("CGL_LIBRARY_DIRS: ${CGL_LIBRARY_DIRS}")
message("FREETYPE_LIBRARY_DIRS: ${FREETYPE_LIBRARY_DIRS}")

#-------------------------------------------------------------------------------
# Add executable
#-------------------------------------------------------------------------------
add_executable(ropesim ${APPLICATION_SOURCE})

target_link_libraries( ropesim
    CGL ${CGL_LIBRARIES}
    glew ${GLEW_LIBRARIES}
    glfw ${GLFW_LIBRARIES}
    ${OPENGL_LIBRARIES}
    ${FREETYPE_LIBRARIES}
    ${CMAKE_THREADS_INIT}
    freetype
)

message("CGL_LIBRARIES: ${CGL_LIBRARIES}")
message("GLEW_LIBRARIES: ${GLEW_LIBRARIES}")
message("GLFW_LIBRARIES: ${GLFW_LIBRARIES}")
message("OPENGL_LIBRARIES: ${OPENGL_LIBRARIES}")
message("FREETYPE_LIBRARIES: ${FREETYPE_LIBRARIES}")
message("CMAKE_THREADS_INIT: ${CMAKE_THREADS_INIT}")

#-------------------------------------------------------------------------------
# Platform-specific configurations for target
#-------------------------------------------------------------------------------
if(APPLE)
  set_property( TARGET ropesim APPEND_STRING PROPERTY COMPILE_FLAGS
                "-Wno-deprecated-declarations -Wno-c++11-extensions")
endif(APPLE)

# Put executable in build directory root
set(EXECUTABLE_OUTPUT_PATH ..)

# Install to project root
install(TARGETS ropesim DESTINATION ${RopeSim_SOURCE_DIR})
