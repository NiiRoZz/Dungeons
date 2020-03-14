cmake_minimum_required(VERSION 3.11)
project(Dungeons
  VERSION 0.1.0
)

find_package(OpenGL REQUIRED)
find_package(glfw3 REQUIRED)
FIND_PACKAGE(glm REQUIRED)

set(DUNGEONS_DATA_DIR "${CMAKE_INSTALL_PREFIX}/share/games/dungeons")
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/src/config.h.in ${CMAKE_CURRENT_BINARY_DIR}/config.h @ONLY)

set(GLAD_DIR "${CMAKE_CURRENT_SOURCE_DIR}/libraries/glad")

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED TRUE)

if(NOT MSVC)
  add_definitions(-Wall -Wextra -g -pedantic)
endif()


add_executable(Dungeons
  src/main.cc
)

target_link_libraries(Dungeons
  glfw
	OpenGL::GL
)

target_include_directories(Dungeons
  PRIVATE
    ${CMAKE_CURRENT_BINARY_DIR}
    "${GLAD_DIR}/include"
)

install(
  TARGETS Dungeons
  RUNTIME DESTINATION games
)

install(
  DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/data/dungeons"
  DESTINATION "${CMAKE_INSTALL_PREFIX}/share/games"
)
