cmake_minimum_required(VERSION 2.8.3)
project(example_rviz_marker)

find_package(catkin_simple REQUIRED)

catkin_simple()
#uncomment the following 4 lines to use the Eigen library

#This is needed as part of the migration to ros jade and later
find_package(Eigen3)
 
# this is depreciated but still necessary for now.
if(NOT EIGEN3_FOUND)
  # Fallback to cmake_modules
  find_package(cmake_modules REQUIRED)
  find_package(Eigen REQUIRED)
  set(EIGEN3_INCLUDE_DIR ${EIGEN_INCLUDE_DIR})
  set(EIGEN_DEP Eigen)
  add_definitions(${EIGEN_DEFINITIONS})
  # Possibly map additional variables to the EIGEN3_ prefix.
else()
  set(EIGEN3_INCLUDE_DIRS ${EIGEN3_INCLUDE_DIR})
  set(EIGEN_DEP Eigen3)
  add_definitions(${EIGEN_DEFINITIONS})
endif()

include_directories(
   ${EIGEN_INCLUDE_DIRS}
 )


# Executables
cs_add_executable(example_rviz_marker src/example_rviz_marker.cpp)
cs_add_executable(triad_display src/triad_display.cpp)
cs_add_executable(triad_display_test_node src/triad_display_test_node.cpp)
cs_install()
cs_export()

