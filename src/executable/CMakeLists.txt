project(executable)

include(conan)
include(add_glsl_shader)

conan_cmake_run(
    REQUIRES
    glfw/3.3.3
    vkfw/1.0.0
    OPTIONS
    vkfw:no_exceptions=True
    BASIC_SETUP CMAKE_TARGETS
    BUILD missing
)

find_package(Vulkan)

set(SOURCES 
    main.cpp
)
add_executable(chess ${SOURCES})

add_glsl_shaders(chess 
    shaders/shader.frag
    shaders/shader.vert
)

target_link_libraries(chess 
    PUBLIC
    renderer
    utils
    Vulkan::Vulkan 
    CONAN_PKG::glfw 
    CONAN_PKG::vkfw
)

