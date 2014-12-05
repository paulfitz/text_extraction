cmake_minimum_required(VERSION 2.8)
project(opencv_sandbox)

# Select a default build configuration if none was chosen
IF(NOT CMAKE_BUILD_TYPE)
  SET(CMAKE_BUILD_TYPE "Release" CACHE STRING "Choose the type of build, options are: None (CMAKE_CXX_FLAGS or CMAKE_C_FLAGS used) Debug Release RelWithDebInfo MinSizeRel." FORCE)
ENDIF()

find_package(OpenCV REQUIRED)

set_property(SOURCE old_ml/old_ml_boost.cpp old_ml/old_ml_data.cpp old_ml/old_ml_inner_functions.cpp old_ml/old_ml_tree.cpp PROPERTY COMPILE_FLAGS -D__OPENCV_BUILD=1)

INCLUDE_DIRECTORIES(${OpenCV_INCLUDE_DIRS} ${CMAKE_SOURCE_DIR}/old_ml)
ADD_EXECUTABLE(text_extraction fast_clustering.cpp group_classifier.cpp main.cpp max_meaningful_clustering.cpp min_bounding_box.cpp mser.cpp nfa.cpp region_classifier.cpp region.cpp old_ml/old_ml_boost.cpp old_ml/old_ml_data.cpp  old_ml/old_ml_inner_functions.cpp old_ml/old_ml_tree.cpp)

FIND_PACKAGE(OpenCV REQUIRED)
IF(OpenCV_FOUND)
  TARGET_LINK_LIBRARIES(text_extraction ${OpenCV_LIBS})
ENDIF()
