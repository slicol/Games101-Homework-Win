cmake_minimum_required(VERSION 3.10)
project(BezierCurve)
set(CMAKE_CXX_STANDARD 14)

#find_package(OpenCV REQUIRED)
include_directories(./../)
include_directories(./../opencv/include)
set(OpenCV_LIBRARIES ${PROJECT_SOURCE_DIR}/../opencv/lib/opencv_world452d.lib)
file(COPY ${PROJECT_SOURCE_DIR}/../opencv/bin/opencv_world452d.dll DESTINATION ${PROJECT_BINARY_DIR}/Debug/)


add_executable(BezierCurve main.cpp)

target_link_libraries(BezierCurve ${OpenCV_LIBRARIES})

