cmake_minimum_required(VERSION 3.20.2)
project(OpenGLTemplate)

option(GLFW_BUILD_DOCS OFF)
option(GLFW_BUILD_EXAMPLES OFF)
option(GLFW_BUILD_TESTS OFF)
add_subdirectory(dependencies/glfw)

# glad
set(GLAD_SOURCES_DIR "dependencies/glad")
add_subdirectory("${GLAD_SOURCES_DIR}/cmake" dependencies/glad)
glad_add_library(glad STATIC REPRODUCIBLE MX API gl:core=4.6)

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

target_link_libraries(
	${PROJECT_NAME}
	PUBLIC
	assimp
	${GLFW_LIBRARIES}
	glad
	glfw)
