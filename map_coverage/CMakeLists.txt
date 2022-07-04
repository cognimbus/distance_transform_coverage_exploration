cmake_minimum_required(VERSION 2.8.3)
project(map_coverage)

add_compile_options(-std=c++14)

find_package(OpenCV REQUIRED )

find_package(catkin REQUIRED COMPONENTS
  
  roscpp  
  nav_msgs
  move_base
  move_base_msgs
  actionlib
  tf
  std_msgs
  roslib
)


catkin_package(
   INCLUDE_DIRS include
   CATKIN_DEPENDS roscpp std_msgs  roslib
)

###########
## Build ##
###########

include_directories(
  ${catkin_INCLUDE_DIRS}
  ${OpenCV_INCLUDE_DIRS}
)

add_executable(map_coverage_node 
    src/map_coverage_ros_node.cpp
    src/AStar.cpp
    src/MoveBaseController.cpp

)

add_dependencies(map_coverage_node
    ${${PROJECT_NAME}_EXPORTED_TARGETS} 
    ${catkin_EXPORTED_TARGETS}
)

target_link_libraries(map_coverage_node
  ${catkin_LIBRARIES}
  ${OpenCV_LIBRARIES}
)
