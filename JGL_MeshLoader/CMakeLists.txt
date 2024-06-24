cmake_minimum_required(VERSION 3.5.1)

project(jgl_demos)

set(CMAKE_CXX_STANDARD 20) # this 

#set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "Build the GLFW example programs")
#set(GLFW_BUILD_TESTS OFF CACHE BOOL "Build the GLFW test programs")
#set(GLFW_BUILD_DOCS OFF CACHE BOOL "Build the GLFW documentation")
#set(GLFW_INSTALL OFF CACHE BOOL "Generate installation target")


file(GLOB APP_SOURCES
    "source/*.h"
    "source/*.cpp"
    "source/elems/*.h"
    "source/elems/*.cpp"
    "source/mesh_import/*.h"
    "source/mesh_import/*.cpp"
    "source/render/*.h"
    "source/render/*.cpp"
    "source/shader/*.h"
    "source/shader/*.cpp"
    "source/ui/*.h"
    "source/ui/*.cpp"
    "source/utils/*.h"
    "source/utils/*.cpp"
    "source/window/*.h"
    "source/window/*.cpp"
    "source/window/*.h"
    "source/window/*.cpp"
    "source/3rdparty/imgui-docking/*.cpp"
    "source/3rdparty/imgui-docking/backends/imgui_impl_glfw.h"
    "source/3rdparty/imgui-docking/backends/imgui_impl_glfw.cpp"
    "source/3rdparty/imgui-docking/backends/imgui_impl_opengl3.h"
    "source/3rdparty/imgui-docking/backends/imgui_impl_opengl3.cpp"
)

add_subdirectory(glfw)
add_subdirectory(assimp/code)

include_directories("glfw/deps") # for glad
include_directories("glfw/include")
include_directories("source/3rdparty/imgui-docking/backends")
include_directories("glm")
include_directories("assimp")
include_directories("source/3rdparty/imgui-docking")
include_directories("source/3rdparty/plugins/imgui")
INCLUDE_DIRECTORIES(/System/Library/Frameworks)

# add_subdirectory(libs/glfw)
include_directories(
    "source"
    "source/elems"
    "source/mesh_import"
    "source/render"
    "source/shader"
    "source/ui"
    "source/utils"
    "source/window"
)

SET(APPLE_LIBS ${APPLE_LIBS} ${GLFW3_LIBRARY} ${OpenGL_LIBRARY} "assimp")

find_package(ASSIMP REQUIRED)
message(STATUS "Found ASSIMP in ${ASSIMP_INCLUDE_DIR}")


FIND_LIBRARY(OpenGL_LIBRARY OpenGL)

# include_directories("libs/glfw/deps") # for glad
# include_directories("libs/glfw/include")
# include_directories("thirdparty")
add_executable(jgl_demos ${APP_SOURCES})

target_link_libraries(jgl_demos "assimp")

if (MSVC)
    add_definitions( "-D _CRT_SECURE_NO_WARNINGS" )
endif()
#if (UNIX)
#    add_definitions( "-std=c99" )
#endif()
target_link_libraries(${PROJECT_NAME} glfw ${GLFW_LIBRARIES})
