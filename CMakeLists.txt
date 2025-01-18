cmake_minimum_required(VERSION 3.16)
project(webviewpy)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib")
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib")

set(CMAKE_MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>")

# include(FetchContent)

# FetchContent_Declare(
#     webview
#     GIT_REPOSITORY https://github.com/webview/webview
#     GIT_TAG 0.12.0)
# FetchContent_MakeAvailable(webview)
add_definitions(-DWEBVIEW_MSWEBVIEW2_BUILTIN_IMPL=0 -DWEBVIEW_MSWEBVIEW2_EXPLICIT_LINK=0)
add_subdirectory(webview)