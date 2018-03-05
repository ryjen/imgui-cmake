cmake_minimum_required(VERSION 3.2)
project(ImGUI)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_SOURCE_DIR}/CMake)
set(CMAKE_DEBUG_POSTFIX "d")

find_package(PkgConfig)

pkg_search_module(SDL2 sdl2)
pkg_search_module(GLFW glfw)
pkg_search_module(GLEW glew)
pkg_search_module(OpenGL opengl)
pkg_search_module(ALLEGRO allegro5)

set(SOURCE_CPP imgui/imgui.cpp imgui/imgui_draw.cpp)
file(GLOB_RECURSE SOURCE_HEADER RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} imgui/*.h  )

add_library(${PROJECT_NAME} SHARED ${SOURCE_CPP} ${SOURCE_HEADER})

target_include_directories(${PROJECT_NAME} SYSTEM PUBLIC imgui)

target_link_libraries(${PROJECT_NAME} ${SDL2_LIBRARY} ${GLFW_LIBRARY} ${GLEW_LIBRARY} ${OPENGL_LIBRARIES})

install(TARGETS ${PROJECT_NAME} DESTINATION lib)

install(FILES ${SOURCE_HEADER} DESTINATION include/imgui)