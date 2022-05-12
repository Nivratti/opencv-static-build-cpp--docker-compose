cmake_minimum_required(VERSION 3.9)

project (demo)

add_definitions(-std=c++11)
add_definitions("-Wall")

set( CMAKE_CXX_FLAGS " -pthread " )

# =============================================================================
# make executable for testing purpose
# -----------------------------------------------------------------------------
add_executable(main
	main_executable.cpp
)

# Find Package
find_package( OpenCV REQUIRED )

# MESSAGE(STATUS ${OpenCV_LIBS})

if( OpenCV_FOUND )
  # target_link_libraries( main ${OpenCV_LIBS})
  # target_link_libraries( main opencv_imgproc opencv_core "-static")
  # target_link_libraries( main opencv_imgcodecs opencv_dnn opencv_objdetect "-static")
  target_link_libraries( main opencv_imgcodecs opencv_dnn opencv_objdetect "-static")
endif()
