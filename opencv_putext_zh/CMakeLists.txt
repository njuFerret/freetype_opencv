cmake_minimum_required(VERSION 3.10)

set( PROJ_NAME cvCnTest)
project(${PROJ_NAME} LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 14)

find_package(OpenCV REQUIRED core highgui)
message("  ${OpenCV_INCLUDE_DIRS}")
message("  ${OpenCV_LIBS}")
include_directories(${OpenCV_INCLUDE_DIRS})

find_package(Freetype REQUIRED)
message("  ${FREETYPE_INCLUDE_DIRS}")
message("  ${FREETYPE_LIBRARIES}")
include_directories(${FREETYPE_INCLUDE_DIRS})

#add_executable(opencvtest opencvtest.cpp CvxFont.cpp Chinese_Test.cpp Japanese_test.cpp symbol_test.cpp)
file(GLOB SRC_LIST *.cpp *.h)


add_executable(${PROJECT_NAME} ${SRC_LIST})


target_link_libraries(${PROJECT_NAME} ${OpenCV_LIBS})
target_link_libraries(${PROJECT_NAME} ${FREETYPE_LIBRARIES})

#set_target_properties(${PROJECT_NAME} PROPERTIES
#  CMAKE_CURRENT_BINARY_DIR
#)

# Copy font files, etc
add_custom_command(
        TARGET ${PROJECT_NAME} POST_BUILD
        COMMAND ${CMAKE_COMMAND} -E copy_directory
                ${CMAKE_CURRENT_SOURCE_DIR}/font/
                ${CMAKE_CURRENT_BINARY_DIR}/font/)

#message(${CMAKE_CURRENT_BINARY_DIR})
