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
if(CMAKE_SYSTEM_NAME STREQUAL "Windows")
    if(${CMAKE_SIZEOF_VOID_P} EQUAL 8)
        set(MSWebView2_LIB ${MSWebView2_INCLUDE_DIR}/../x64/WebView2LoaderStatic.lib)
        set(YY_Thunks_for_Win7 ${CMAKE_CURRENT_SOURCE_DIR}/YY-Thunks/objs/x64/YY_Thunks_for_Win7.obj)
    else()
        set(MSWebView2_LIB ${MSWebView2_INCLUDE_DIR}/../x86/WebView2LoaderStatic.lib)
        set(YY_Thunks_for_Win7 ${CMAKE_CURRENT_SOURCE_DIR}/YY-Thunks/objs/x86/YY_Thunks_for_Win7.obj)
    endif()
    set(ExtraLibs ${MSWebView2_LIB} ${YY_Thunks_for_Win7})
endif()
target_link_libraries(webview_core_shared PRIVATE  ${ExtraLibs})