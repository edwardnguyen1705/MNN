IF(MNN_BUILD_OPENCV)
  option(MNN_IMGCODECS "Enable imgcodecs" OFF)
  option(MNN_OPENCV_TEST "Enable opencv test" OFF)

  SET(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/../../)
  include_directories(${CMAKE_CURRENT_LIST_DIR}/include/)
  include_directories(${CMAKE_CURRENT_LIST_DIR}/../../3rd_party/imageHelper/)

  # include(${CMAKE_CURRENT_LIST_DIR}/test/CMakeLists.txt)
  if(${MNN_OPENCV_TEST})
    add_subdirectory(${CMAKE_CURRENT_LIST_DIR}/test)
  endif()

  file(GLOB_RECURSE IMGPROC_SRC ${CMAKE_CURRENT_LIST_DIR}/source/imgproc/*.cpp ${CMAKE_CURRENT_LIST_DIR}/include/imgproc/*.hpp)
  if(${MNN_IMGCODECS})
    file(GLOB_RECURSE IMGCODECS_SRC ${CMAKE_CURRENT_LIST_DIR}/source/imgcodecs/*.cpp ${CMAKE_CURRENT_LIST_DIR}/include/imgcodecs/*.hpp)
  endif()

  IF(MNN_BUILD_SHARED_LIBS)
    add_library(MNNOpenCV SHARED ${IMGPROC_SRC} ${IMGCODECS_SRC})
    target_link_libraries(MNNOpenCV MNN MNN_Express)
  ELSE()
    add_library(MNNOpenCV STATIC ${IMGPROC_SRC} ${IMGCODECS_SRC})
  ENDIF()
ENDIF()
