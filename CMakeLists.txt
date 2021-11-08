cmake_minimum_required(VERSION 3.20.2)
project(OpenGLTemplate)

option(GLFW_BUILD_DOCS OFF)
option(GLFW_BUILD_EXAMPLES OFF)
option(GLFW_BUILD_TESTS OFF)
option(GLFW_INSTALL OFF)
add_subdirectory(dependencies/glfw)

# glad
add_subdirectory(dependencies/glad/cmake)

glad_add_library(glad REPRODUCIBLE MX LANGUAGE "c++" API gl:core=4.6)

include_directories(
	dependencies/glfw/include/)
	
add_executable(${PROJECT_NAME} src/main.cpp)

target_link_libraries(${PROJECT_NAME} PUBLIC
	glad
	glfw)
