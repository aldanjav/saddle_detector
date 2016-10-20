cmake_minimum_required(VERSION 2.8)
PROJECT( saddle_detector_project )
FIND_PACKAGE( OpenCV REQUIRED )

if(CMAKE_COMPILER_IS_GNUCXX)
    add_definitions(-std=c++11)
endif()

message("OCV includes: ${OpenCV_INCLUDE_DIRS}")
ADD_EXECUTABLE( saddlepts saddlepts.cpp anyoption.cpp sorb.cpp fast.cpp fast_score.cpp )
TARGET_LINK_LIBRARIES( saddlepts ${OpenCV_LIBS} )
