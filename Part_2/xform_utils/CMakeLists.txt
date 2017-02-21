cmake_minimum_required(VERSION 2.8.3)
project(xform_utils)

find_package(catkin_simple REQUIRED)

#uncomment next line to use OpenCV library
#find_package(OpenCV REQUIRED)

#uncomment the next 2 lines to use the point-cloud library
#find_package(PCL 1.7 REQUIRED)
#include_directories(${PCL_INCLUDE_DIRS})

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

catkin_simple()

# example boost usage
# find_package(Boost REQUIRED COMPONENTS system thread)

# C++0x support - not quite the same as final C++11!
# use carefully;  can interfere with point-cloud library
# SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++0x")

# Libraries: uncomment the following and edit arguments to create a new library
cs_add_library(xform_utils src/xform_utils.cpp)   

# Executables: uncomment the following and edit arguments to compile new nodes
# may add more of these lines for more nodes from the same package
cs_add_executable(example_xform_utils src/example_xform_utils.cpp)

#the following is required, if desire to link a node in this package with a library created in this same package
# edit the arguments to reference the named node and named library within this package
target_link_libraries(example_xform_utils xform_utils)

cs_install()
cs_export()
    
