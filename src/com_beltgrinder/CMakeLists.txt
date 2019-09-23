cmake_minimum_required(VERSION 2.8.3)
project(com_beltgrinder)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  std_msgs
)
catkin_package(
  INCLUDE_DIRS include
#  LIBRARIES com_beltgrinder
#  CATKIN_DEPENDS other_catkin_pkg
#  DEPENDS system_lib
)

include_directories (
  include ${catkin_INCLUDE_DIRS}
  include 
  ${catkin_INCLUDE_DIRS}
  ${com_beltgrinder_INCLUDE_DIRS}
  ${CMAKE_CURRENT_BINARY_DIR})
link_directories    (${com_beltgrinder_LIBRARY_DIRS})
add_definitions     (${com_beltgrinder_DEFINITIONS})

set  (project_SOURCES src/main.cpp)
#set  (project_HEADERS include/)
#set  (project_FORMS   src/mainwindow.ui)

# Find includes in corresponding build directories
#set(CMAKE_INCLUDE_CURRENT_DIR ON)
#set(CMAKE_C_FLAGS_DEBUG MTd)
add_compile_options(-std=c++11)
# Instruct CMake to run moc automatically when needed.
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)

# Find the QtWidgets library

set(CMAKE_PREFIX_PATH /home/proj/Qt5.8.0/5.8/gcc_64)
find_package(Qt5Widgets REQUIRED)

add_library(AdsLib STATIC 
  include/AdsLib/AdsDef.cpp
  include/AdsLib/AdsLib.cpp
  include/AdsLib/AmsConnection.cpp
  include/AdsLib/AmsPort.cpp
  include/AdsLib/AmsRouter.cpp
  include/AdsLib/Log.cpp
  include/AdsLib/NotificationDispatcher.cpp
  include/AdsLib/Sockets.cpp
  include/AdsLib/Frame.cpp)

add_executable  (com_beltgrinder src/main.cpp src/com_beltgrinder.cpp)

add_dependencies(com_beltgrinder ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})
target_link_libraries (com_beltgrinder AdsLib Qt5::Widgets pthread ${catkin_LIBRARIES})