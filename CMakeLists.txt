cmake_minimum_required(VERSION 3.17)
project(test_github_actions)

set(CMAKE_CXX_STANDARD 14)


if (APPLE)
    set(TARGET_NAME "hello_darwin")
elseif (WIN32)
    if(CMAKE_SIZEOF_VOID_P EQUAL "8")
        # 64 bits
        set(TARGET_NAME "hello_windows_x64")
    elseif(CMAKE_SIZEOF_VOID_P EQUAL "4")
        # 32 bits
        set(TARGET_NAME "hello_windows_x86")
    endif()
elseif (UNIX AND NOT APPLE)
    set(TARGET_NAME "hello_linux")
else ()
    message(FATAL_ERROR "Unsupported system ${CMAKE_SYSTEM_NAME}")
endif ()

add_executable(${TARGET_NAME} main.cpp)