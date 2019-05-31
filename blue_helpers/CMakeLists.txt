cmake_minimum_required(VERSION 2.8.3)
project(blue_helpers)

## Compile as C++11, supported in ROS Kinetic and newer
add_compile_options(-std=c++14)
set(GCC_COVERAGE_COMPILE_FLAGS "-fpermissive")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${GCC_COVERAGE_COMPILE_FLAGS} ${GAZEBO_CXX_FLAGS}" )

find_package(catkin REQUIRED COMPONENTS
  rospy
  roscpp
  moveit_core
  moveit_visual_tools
  moveit_ros_planning
  moveit_ros_planning_interface
  joint_state_controller
  joint_state_publisher
  joint_trajectory_controller
  trajectory_msgs
  control_msgs
  sensor_msgs
  actionlib
  actionlib_msgs
)

catkin_package(
  CATKIN_DEPENDS 
  moveit_core
  moveit_visual_tools
  moveit_ros_planning_interface
)
catkin_python_setup()

include_directories(
  include
  ${catkin_INCLUDE_DIRS}
)

add_library(moveit_arm_utils include/moveit_arm_utils.cpp)

add_executable(right_end_effector_pose_reporter src/right_end_effector_pose_reporter.cpp)
target_link_libraries(right_end_effector_pose_reporter moveit_arm_utils ${catkin_LIBRARIES})

add_executable(left_end_effector_pose_reporter src/left_end_effector_pose_reporter.cpp)
target_link_libraries(left_end_effector_pose_reporter moveit_arm_utils ${catkin_LIBRARIES})

add_dependencies(right_end_effector_pose_reporter moveit_arm_utils ${blue_moveit_gazebo_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})
add_dependencies(left_end_effector_pose_reporter moveit_arm_utils ${blue_moveit_gazebo_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})
