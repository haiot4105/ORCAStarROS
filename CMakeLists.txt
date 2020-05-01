# TODO refactor CMakeLists.txtx

cmake_minimum_required(VERSION 3.5)
set (CMAKE_PREFIX_PATH "/opt/ros/kinetic")
include($ENV{ROS_ROOT}/core/rosbuild/rosbuild.cmake)
set (CMAKE_CXX_STANDARD 14)

# Set the build type.  Options are:
#  Coverage       : w/ debug symbols, w/o optimization, w/ code-coverage
#  Debug          : w/ debug symbols, w/o optimization
#  Release        : w/o debug symbols, w/ optimization
#  RelWithDebInfo : w/ debug symbols, w/ optimization
#  MinSizeRel     : w/o debug symbols, w/ optimization, stripped binaries
#set(ROS_BUILD_TYPE RelWithDebInfo)

rosbuild_init()

#set the default path for built executables to the "bin" directory
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
#set the default path for built libraries to the "lib" directory
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

add_subdirectory(ORCAStarLib)

include_directories(./ORCAStarLib/Src)


rosbuild_genmsg()
rosbuild_gensrv()


rosbuild_add_executable(ROSSimActor src/StartActor.cpp src/ROSSimActor.h src/ROSSimActor.cpp)
rosbuild_add_executable(ROSMission src/StartMission.cpp src/ROSMission.h src/ROSMission.cpp)
rosbuild_add_executable(ROSAgent src/StartAgent.cpp src/ROSAgent.h src/ROSAgent.cpp)
rosbuild_add_executable(ROSVisualization src/StartVisualization.cpp)

target_link_libraries(ROSSimActor ORCAStarLib TINYXML)
target_link_libraries(ROSMission ORCAStarLib TINYXML)
target_link_libraries(ROSAgent ORCAStarLib TINYXML)


#common commands for building c++ executables and libraries
#rosbuild_add_library(${PROJECT_NAME} src/example.cpp)
#target_link_libraries(${PROJECT_NAME} another_library)
#rosbuild_add_boost_directories()
#rosbuild_link_boost(${PROJECT_NAME} thread)
#rosbuild_add_executable(example examples/example.cpp)
#target_link_libraries(example ${PROJECT_NAME})