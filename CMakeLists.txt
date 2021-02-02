cmake_minimum_required(VERSION 3.10)
project(GLFWCMake VERSION 1.0)

add_executable(${PROJECT_NAME} src/main.cpp)

target_compile_features(${PROJECT_NAME} PUBLIC cxx_constexpr)
target_include_directories(${PROJECT_NAME} PUBLIC
                           "${CMAKE_SOURCE_DIR}/src"
                           )

set(CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

set(CMAKE_CXX_FLAGS "-stdlib=libc++")
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS} -O0 -g -v -Wall -Wextra -Wno-long-long -pedantic")
set(CMAKE_CXX_FLAGS_RELEASE "{CMAKE_CXX_FLAGS} -O3")
set(CMAKE_CXX_FLAGS_MINSIZEREL "{CMAKE_CXX_FLAGS} -Os")
set(CMAKE_CXX_FLAGS_RELWITHDEBINFO "{CMAKE_CXX_FLAGS} -Og -g")

# https://cmake.org/cmake/help/latest/module/FindOpenGL.html
set(OpenGL_GL_PREFERENCE "GLVND")
# glfw3
find_package(glfw3 3.3 REQUIRED)
find_package(OpenGL REQUIRED)

target_link_libraries(${PROJECT_NAME} 
                        glfw
                        OpenGL::GL
                    )