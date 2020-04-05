cmake_minimum_required(VERSION 3.14)
PROJECT( saddle_detector_project )
FIND_PACKAGE( OpenCV REQUIRED )

cmake_policy(SET CMP0037 NEW)
set(CMAKE_CXX_STANDARD 11)

add_subdirectory(src)

find_package (Python3 COMPONENTS Interpreter Development NumPy)

set(OpenCV_BINARY_DIR src)

if (Python3_FOUND AND SWIG_FOUND)
    add_subdirectory(python)
endif()
