project(Imgui)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++17")

# Use a more specific file pattern to avoid unintended matches
file(GLOB IMGUI_CORE_SRC
    "${CMAKE_CURRENT_SOURCE_DIR}/*.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/*.h"
)

# Use specific file patterns for each subdirectory to avoid unintended matches
file(GLOB IMGUI_MISC_CPP_SRC
    "${CMAKE_CURRENT_SOURCE_DIR}/misc/cpp/*.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/misc/cpp/*.h"
)

file(GLOB IMGUI_MISC_DEBUGGERS_SRC
    "${CMAKE_CURRENT_SOURCE_DIR}/misc/debuggers/*.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/misc/debuggers/*.h"
)

file(GLOB IMGUI_MISC_FONTS_SRC
    "${CMAKE_CURRENT_SOURCE_DIR}/misc/fonts/*.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/misc/fonts/*.h"
    "${CMAKE_CURRENT_SOURCE_DIR}/misc/freetype/*.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/misc/freetype/*.h"
)

file(GLOB IMGUI_MISC_SINGLE_FILE_SRC
    "${CMAKE_CURRENT_SOURCE_DIR}/misc/single_file/*.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/misc/single_file/*.h"
)

# Gather the source files into a single list
set(SRC
    ${IMGUI_CORE_SRC}
    ${IMGUI_MISC_CPP_SRC}
    ${IMGUI_MISC_DEBUGGERS_SRC}
    ${IMGUI_MISC_FONTS_SRC}
    ${IMGUI_MISC_SINGLE_FILE_SRC}
)

# Add backend-specific source files directly
list(APPEND SRC
    "${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_glfw.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_glfw.h"
    "${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_opengl3_loader.h"
    "${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_opengl3.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_opengl3.h"
)

if(XCODE)
    add_definitions(-std=c++17) 
    list(APPEND SRC
        "${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_osx.h"
        "${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_osx.mm"
    )
endif()

add_library(imgui ${SRC})
include_directories(${ENGINE_PATH}/lib/glfw/include)
include_directories(${ENGINE_PATH}/lib/freetype/include)
target_include_directories(imgui PUBLIC .)