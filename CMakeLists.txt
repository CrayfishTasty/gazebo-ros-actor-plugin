cmake_minimum_required(VERSION 3.5)
project(gazebo_ros_actor_plugin)

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()
if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# Find packages
find_package(ament_cmake REQUIRED)
find_package(std_msgs REQUIRED)
find_package(gazebo_ros REQUIRED)
find_package(gazebo_dev REQUIRED) 
find_package(geometry_msgs REQUIRED)
find_package(nav_msgs REQUIRED)
find_package(rclcpp REQUIRED)
find_package(tf2 REQUIRED)
find_package(tf2_ros REQUIRED)
find_package(tf2_geometry_msgs REQUIRED)


# Include directories
include_directories(
  include
  ${gazebo_dev_INCLUDE_DIRS}
  ${gazebo_ros_INCLUDE_DIRS}
)

# Link directories
link_directories(${GAZEBO_LIBRARY_DIRS})

# Add library
add_library(gazebo_ros_actor_command SHARED src/gazebo_ros_actor_command.cpp)
ament_target_dependencies(gazebo_ros_actor_command
  rclcpp
  gazebo_ros
  gazebo_dev
  geometry_msgs
  nav_msgs
  tf2
  tf2_ros
  tf2_geometry_msgs
)

# Link libraries
target_link_libraries(gazebo_ros_actor_command
  ${GAZEBO_LIBRARIES}
  ${gazebo_ros_LIBRARIES}
)

# Install
install(TARGETS gazebo_ros_actor_command
  DESTINATION lib/${PROJECT_NAME})

# Export dependencies
ament_export_dependencies(ament_cmake)
ament_export_dependencies(gazebo_ros)
ament_export_dependencies(gazebo_dev)
ament_export_dependencies(geometry_msgs)
ament_export_dependencies(nav_msgs)
ament_export_dependencies(rclcpp)
ament_export_dependencies(tf2)
ament_export_dependencies(tf2_ros)
ament_export_dependencies(tf2_geometry_msgs)
ament_package()
