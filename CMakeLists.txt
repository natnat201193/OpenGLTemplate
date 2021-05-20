cmake_minimum_required(VERSION 3.20.2)
project(OpenGLTemplate)

option(GLFW_BUILD_DOCS OFF)
option(GLFW_BUILD_EXAMPLES OFF)
option(GLFW_BUILD_TESTS OFF)
add_subdirectory(dependencies/glfw)

# glad
add_subdirectory("dependencies/glad/cmake" glad_cmake)
glad_add_library(glad_gl_core_33 REPRODUCIBLE API gl:core=3.3)

option(ASSIMP_BUILD_ASSIMP_TOOLS OFF)
option(ASSIMP_BUILD_SAMPLES OFF)
option(ASSIMP_BUILD_TESTS OFF)
add_subdirectory(dependencies/assimp)

include_directories(
	dependencies/assimp/include/
	dependencies/glfw/include/
	dependencies/glm/
	dependencies/stb/)
	
add_executable(${PROJECT_NAME} src/main.cpp)

target_link_libraries(${PROJECT_NAME} PUBLIC
	assimp
	glad_gl_core_mx_33
	glfw)
