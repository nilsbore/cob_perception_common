cmake_minimum_required(VERSION 2.8.3)
project(cob_vision_utils)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
find_package(catkin REQUIRED COMPONENTS
  cmake_modules
  roscpp
  visualization_msgs
)

find_package(OpenCV REQUIRED)

###################################
## catkin specific configuration ##
###################################
## The catkin_package macro generates cmake config files for your package
## Declare things to be passed to dependent projects
## INCLUDE_DIRS: uncomment this if you package contains header files
## LIBRARIES: libraries you create in this project that dependent projects also need
## CATKIN_DEPENDS: catkin_packages dependent projects also need
## DEPENDS: system dependencies of this project that dependent projects also need
catkin_package(
  INCLUDE_DIRS
    common/include
    ros/include
  LIBRARIES
    cob_vision_utils
  CATKIN_DEPENDS
    roscpp
    visualization_msgs
  DEPENDS
    OpenCV
)

###########
## Build ##
###########

## Specify additional locations of header files
## Your package locations should be listed before other locations
# include_directories(include ${catkin_INCLUDE_DIRS} ${Boost_INCLUDE_DIRS})
include_directories(
  common/include
  ros/include
  ${OpenCV_INCLUDE_DIRS}
)

## Declare a cpp library
add_library(cob_vision_utils
  common/src/VisionUtils.cpp
  common/src/CameraSensorToolbox.cpp
)

## Specify libraries to link a library or executable target against
target_link_libraries(cob_vision_utils
  ${OpenCV_LIBS}
  tinyxml
)


# set build flags for targets
set_target_properties(cob_vision_utils PROPERTIES COMPILE_FLAGS "-D__LINUX__ -D__COB_ROS__")

