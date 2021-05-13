cmake_minimum_required(VERSION 3.20.2)
project(OpenGLTemplate)

option(GLFW_BUILD_DOCS OFF)
option(GLFW_BUILD_EXAMPLES OFF)
option(GLFW_BUILD_TESTS OFF)
add_subdirectory(dependencies/glfw)

# glad
option(GLAD_EXPORT OFF)
add_subdirectory(Dependencies/glad)

option(ASSIMP_BUILD_ASSIMP_TOOLS OFF)
option(ASSIMP_BUILD_SAMPLES OFF)
option(ASSIMP_BUILD_TESTS OFF)
add_subdirectory(dependencies/assimp)

if(MSVC)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /W4")
else()
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wextra -Wpedantic -std=c++11")
    if(NOT WIN32)
        set(GLAD_LIBRARIES dl)
    endif()
endif()

include_directories(
	dependencies/assimp/include/
	dependencies/glad/include/
	dependencies/glfw/include/
	dependencies/glm/
	dependencies/stb/)
	
add_executable(${PROJECT_NAME} src/main.cpp)

target_link_libraries(
	${PROJECT_NAME} 
	assimp
	glfw
	${GLFW_LIBRARIES}
	${GLAD_LIBRARIES})
