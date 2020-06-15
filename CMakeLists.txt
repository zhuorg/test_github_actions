cmake_minimum_required(VERSION 3.0)
project(test_github_actions)

set(CMAKE_CXX_STANDARD 14)


if (APPLE)

    set(TARGET_NAME "hello_darwin")
    add_executable(${TARGET_NAME} main.cpp)

elseif (WIN32)

    configure_file("${CMAKE_CURRENT_SOURCE_DIR}/assets/icon.ico" "${CMAKE_CURRENT_BINARY_DIR}/icon.ico" COPYONLY)
    configure_file("${CMAKE_CURRENT_SOURCE_DIR}/win32.rc.in" "${CMAKE_CURRENT_BINARY_DIR}/win32.rc" @ONLY)

    if(CMAKE_SIZEOF_VOID_P EQUAL "8")
        # 64 bits
        set(TARGET_NAME "hello_windows_x64")
    elseif(CMAKE_SIZEOF_VOID_P EQUAL "4")
        # 32 bits
        set(TARGET_NAME "hello_windows_x86")
    endif()

    add_executable(${TARGET_NAME} main.cpp "${CMAKE_CURRENT_BINARY_DIR}/win32.rc")

elseif (UNIX AND NOT APPLE)

    set(TARGET_NAME "hello_linux")
    add_executable(${TARGET_NAME} main.cpp)

else ()
    message(FATAL_ERROR "Unsupported system ${CMAKE_SYSTEM_NAME}")
endif ()

