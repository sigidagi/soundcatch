cmake_minimum_required (VERSION 2.6)
project (test_world)

include_directories(${CMAKE_SOURCE_DIR}/../..
                    ${FFMPEG_INCLUDE_DIRS}

)


add_executable(test_world main.cpp

)

target_link_libraries(test_world ${FFMPEG_LIBRARIES})
