
#IF(CMAKE_COMPILER_IS_GNUCXX)
  #SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wno-strict-aliasing")
  #SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wextra -Wno-write-strings")
  #SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wno-deprecated -ansi")
  ##SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O3 -ftree-vectorize -funroll-loops")
    #add_definitions(-std=c++11)
#ENDIF(CMAKE_COMPILER_IS_GNUCXX)

message("OCV includes: ${OpenCV_INCLUDE_DIRS}")

add_executable(saddlepts-bin saddlepts.cpp anyoption.cpp lbq.cpp sorb.cpp fast.cpp fast_score.cpp)
target_include_directories(saddlepts-bin PRIVATE ${OpenCV_INCLUDE_DIRS})

TARGET_LINK_LIBRARIES(saddlepts-bin ${OpenCV_LIBS})
set_target_properties(saddlepts-bin PROPERTIES OUTPUT_NAME saddlepts)
