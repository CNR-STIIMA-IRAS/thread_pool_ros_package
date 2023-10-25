cmake_minimum_required(VERSION 3.0.2)
project(thread_pool_ros_package)

if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Release)
endif()

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

find_package(catkin REQUIRED COMPONENTS roscpp) 

catkin_package(
  INCLUDE_DIRS include
  CATKIN_DEPENDS roscpp
)

## Add headers files
include_directories (
	include
	${catkin_INCLUDE_DIRS}
)
 
set(HEADERS include/thread_pool_ros_package/SafeQueue.h include/thread_pool_ros_package/ThreadPool.h)
 set(SOURCES example/main.cpp)
SET(CMAKE_CXX_FLAGS -pthread)
 
# main.cpp
add_executable(main ${HEADERS} ${SOURCES})
target_link_libraries(main)

#############
## Install ##
#############

install(DIRECTORY include/${PROJECT_NAME}/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
  FILES_MATCHING PATTERN "*.h"
  PATTERN ".svn" EXCLUDE
)


