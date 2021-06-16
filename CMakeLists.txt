cmake_minimum_required(VERSION 3.0.0)
project(opengl1 VERSION 0.1.0)

cmake_policy(SET CMP0079 NEW)

include(CTest)
enable_testing()

set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "Build the GLFW example programs")
set(GLFW_BUILD_TESTS OFF CACHE BOOL "Build the GLFW test programs")
set(GLFW_BUILD_DOCS OFF CACHE BOOL "Build the GLFW documentation")
set(GLFW_INSTALL OFF CACHE BOOL "Generate installation target")

add_subdirectory("src")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/libs")

target_include_directories(opengl1
    PRIVATE "${CMAKE_CURRENT_SOURCE_DIR}/libs/glfw-3.3.4/include")

find_package(OpenGL REQUIRED)

target_link_libraries(opengl1 PRIVATE ${OPENGL_gl_LIBRARY})
target_link_libraries(opengl1 PRIVATE glad)
target_link_libraries(opengl1 PRIVATE glfw)

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)
