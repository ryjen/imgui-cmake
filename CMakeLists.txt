cmake_minimum_required(VERSION 3.2)

project(imgui)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_SOURCE_DIR}/CMake)

find_package(PkgConfig)

pkg_search_module(SDL2 sdl2)
pkg_search_module(GLFW glfw)
pkg_search_module(GLEW glew)
pkg_search_module(OPENGL opengl)
pkg_search_module(ALLEGRO allegro5)

file(GLOB_RECURSE SOURCE_HEADER RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} imgui/*.h  )

# build main library

add_library(${PROJECT_NAME} SHARED imgui/imgui.cpp imgui/imgui_draw.cpp ${SOURCE_HEADER})

target_include_directories(${PROJECT_NAME} SYSTEM PUBLIC imgui)

target_link_libraries(${PROJECT_NAME} ${SDL2_LIBRARY} ${GLFW_LIBRARY} ${GLEW_LIBRARY} ${OPENGL_LIBRARY} ${ALLEGRO_LIBRARY})

# build demo library

add_library(${PROJECT_NAME}_demo SHARED imgui/imgui_demo.cpp ${SOURCE_HEADER})

target_include_directories(${PROJECT_NAME}_demo SYSTEM PUBLIC imgui)

target_link_libraries(${PROJECT_NAME}_demo ${PROJECT_NAME})

# install targets

install(TARGETS ${PROJECT_NAME} ${PROJECT_NAME}_demo DESTINATION lib)

install(FILES ${SOURCE_HEADER} DESTINATION include/imgui)