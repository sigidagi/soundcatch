cmake_minimum_required (VERSION 2.6)
SET(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH}
                      ${CMAKE_SOURCE_DIR}/cmake)

project (soundcatch)

find_package(Boost REQUIRED)
find_package(FFTW3 REQUIRED)
find_package(FFmpeg REQUIRED)



# needed bu ffmpeg
add_definitions(-D__STDC_CONSTANT_MACROS) 

SET(CMAKE_VERBOSE_MAKEFILE off)

include_directories(${CMAKE_SOURCE_DIR}
                    $ENV{HOME}/local/include
                    ${Boost_INCLUDE_DIRS}
                    ${FFMPEG_INCLUDE_DIRS}
)


message(STATUS "ffmpeg directories: " ${FFMPEG_INCLUDE_DIRS})
message(STATUS "ffmpeg libraries: " ${FFMPEG_LIBRARIES})
message(STATUS "ffmpeg library dirs: " ${FFMPEG_LIBRARY_DIRS})


link_directories($ENV{HOME}/local/lib)

IF(EXISTS $ENV{INSTALL_PREFIX})
  set(CMAKE_INSTALL_PREFIX $ENV{INSTALL_PREFIX} CACHE PATH "Install prefix")
ENDIF(EXISTS $ENV{INSTALL_PREFIX})
message(STATUS "Install prefix: " ${CMAKE_INSTALL_PREFIX})


IF (${CMAKE_C_COMPILER_ID} MATCHES GNU)
   add_definitions(-W -Wall -Wextra)
ENDIF()

add_library(soundcatch
  soundcatch/encoder.cpp
  soundcatch/decoder.cpp
)

add_subdirectory(test)

install(TARGETS soundcatch DESTINATION lib/)
install(TARGETS soundcatch DESTINATION lib/Debug CONFIGURATIONS Debug)
install(TARGETS soundcatch DESTINATION lib/Release CONFIGURATIONS Release)

install(DIRECTORY soundcatch DESTINATION include
  FILES_MATCHING PATTERN "*.h")
install(DIRECTORY soundcatch DESTINATION include
  FILES_MATCHING PATTERN "*.hpp")
