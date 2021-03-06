cmake_minimum_required(VERSION 2.4.6)
include($ENV{ROS_ROOT}/core/rosbuild/rosbuild.cmake)
rosbuild_find_ros_package(rtmbuild)
include(${rtmbuild_PACKAGE_PATH}/cmake/rtmbuild.cmake)

rosbuild_init()

# Set the build type.  Options are:
#  Coverage       : w/ debug symbols, w/o optimization, w/ code-coverage
#  Debug          : w/ debug symbols, w/o optimization
#  Release        : w/o debug symbols, w/ optimization
#  RelWithDebInfo : w/ debug symbols, w/ optimization
#  MinSizeRel     : w/o debug symbols, w/ optimization, stripped binaries
#set(ROS_BUILD_TYPE RelWithDebInfo)

#set the default path for built executables to the "bin" directory
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
#set the default path for built libraries to the "lib" directory
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

#uncomment if you have defined messages
#rosbuild_genmsg()
#uncomment if you have defined services
#rosbuild_gensrv()

#common commands for building c++ executables and libraries
#rosbuild_add_library(${PROJECT_NAME} src/example.cpp)
#target_link_libraries(${PROJECT_NAME} another_library)
#rosbuild_add_boost_directories()
#rosbuild_link_boost(${PROJECT_NAME} thread)
#rosbuild_add_executable(example examples/example.cpp)
#target_link_libraries(example ${PROJECT_NAME})

rosbuild_find_ros_package("openhrp3")
configure_file(${PROJECT_SOURCE_DIR}/models/SampleRobot.conf.in
  ${PROJECT_SOURCE_DIR}/models/SampleRobot.conf)
configure_file(${PROJECT_SOURCE_DIR}/models/SampleRobot.xml.in
  ${PROJECT_SOURCE_DIR}/models/SampleRobot.xml)
##
## tests
##
rosbuild_find_ros_package("hrpsys")
if(EXISTS ${hrpsys_PACKAGE_PATH}/share/hrpsys/samples/HRP4C/HRP4Cmain.wrl)
  rosbuild_add_rostest(test/hrp4c-test.launch)
endif()
rosbuild_add_rostest(test/pa10-test.launch)
rosbuild_add_rostest(test/samplerobot-test.launch)

