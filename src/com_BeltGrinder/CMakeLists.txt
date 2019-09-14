cmake_minimum_required(VERSION 2.8.3)
project(com_BeltGrinder)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  std_msgs
)

#set(CMAKE_CXX_STANDARD 11)

include_directories (
  include ${catkin_INCLUDE_DIRS}${com_BeltGrinder_INCLUDE_DIRS})
link_directories    (${com_BeltGrinder_LIBRARY_DIRS})
add_definitions     (${com_BeltGrinder_DEFINITIONS})

set  (project_SOURCES src/main.cpp)
#set  (project_HEADERS include/)
#set  (project_FORMS   src/mainwindow.ui)

# Find includes in corresponding build directories
set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_C_FLAGS_DEBUG MTd)
add_compile_options(-std=c++11)
# Instruct CMake to run moc automatically when needed.
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)

# Find the QtWidgets library
set(CMAKE_PREFIX_PATH /opt/Qt/5.4/)
if("${qt_gui_cpp_USE_QT_MAJOR_VERSION} " STREQUAL "5 ")
find_package(Qt5Widgets REQUIRED)
else()
find_package(Qt4 COMPONENTS QtCore QtGui REQUIRED)
include(${QT_USE_FILE})
endif()

add_executable  (com_BeltGrinder
  src/main.cpp ${project_SOURCES} ${project_HEADERS})
link_directories(com_BeltGrinder include/AdsLib/)
link_libraries(include/AdsLib/libAds-Linux.a)
target_link_libraries (com_BeltGrinder libAds-Linux.a Qt5::Widgets)
