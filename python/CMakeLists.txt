set(PYTHON_SOURCE_DIR "${CMAKE_CURRENT_SOURCE_DIR}")

set(cv2_generated_files
    "${CMAKE_CURRENT_BINARY_DIR}/pyopencv_generated_enums.h"
    "${CMAKE_CURRENT_BINARY_DIR}/pyopencv_generated_funcs.h"
    "${CMAKE_CURRENT_BINARY_DIR}/pyopencv_generated_include.h"
    "${CMAKE_CURRENT_BINARY_DIR}/pyopencv_generated_modules.h"
    "${CMAKE_CURRENT_BINARY_DIR}/pyopencv_generated_modules_content.h"
    "${CMAKE_CURRENT_BINARY_DIR}/pyopencv_generated_types.h"
    "${CMAKE_CURRENT_BINARY_DIR}/pyopencv_generated_types_content.h"
    "${CMAKE_CURRENT_BINARY_DIR}/pyopencv_generated_signatures.h"
)

configure_file(
    ${PYTHON_SOURCE_DIR}/headers.txt.in
    ${CMAKE_CURRENT_BINARY_DIR}/headers.txt
)

add_custom_command(
    OUTPUT ${cv2_generated_files}
    COMMAND "${Python3_EXECUTABLE}" "${PYTHON_SOURCE_DIR}/src2/gen2.py" "${CMAKE_CURRENT_BINARY_DIR}" "${CMAKE_CURRENT_BINARY_DIR}/headers.txt"
    DEPENDS "${PYTHON_SOURCE_DIR}/src2/gen2.py"
            "${PYTHON_SOURCE_DIR}/src2/hdr_parser.py"
            # not a real build dependency (file(WRITE) result): ${CMAKE_CURRENT_BINARY_DIR}/headers.txt
            # ${opencv_hdrs}
    COMMENT "Generate files for Python bindings and documentation"
)

add_custom_target(gen_opencv_python_source ALL DEPENDS ${cv2_generated_files})

set(SOURCE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../src")
add_library(pysaddlepts
MODULE
${PYTHON_SOURCE_DIR}/src2/cv2.cpp
${SOURCE_DIR}/saddlepts.cpp
${SOURCE_DIR}/anyoption.cpp
${SOURCE_DIR}/lbq.cpp
${SOURCE_DIR}/sorb.cpp
${SOURCE_DIR}/fast.cpp
${SOURCE_DIR}/fast_score.cpp
)

target_include_directories(pysaddlepts PRIVATE ${OpenCV_INCLUDE_DIRS})
target_include_directories(pysaddlepts PRIVATE ${Python3_INCLUDE_DIRS})
target_include_directories(pysaddlepts PRIVATE ${Python3_NumPy_INCLUDE_DIRS})
target_include_directories(pysaddlepts PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/include)
target_include_directories(pysaddlepts PRIVATE ${CMAKE_CURRENT_BINARY_DIR})
target_include_directories(pysaddlepts PRIVATE ${SOURCE_DIR})

TARGET_LINK_LIBRARIES(pysaddlepts ${OpenCV_LIBS} ${Python3_LIBRARIES})

# remove the lib prefix
SET_TARGET_PROPERTIES(pysaddlepts PROPERTIES PREFIX "")

MESSAGE("CURRENT BIN DIR" ${CMAKE_CURRENT_BINARY_DIR})

add_dependencies(pysaddlepts gen_opencv_python_source)

# configure test python script
set(PYSADDLEPTS_BUILD_PATH ${CMAKE_CURRENT_BINARY_DIR})
configure_file(
    ${PYTHON_SOURCE_DIR}/test/pysaddletest.py.in
    ${PROJECT_SOURCE_DIR}/pysaddletest.py
)
