cmake_minimum_required(VERSION 3.25)

project(xray-serialization VERSION 1.0.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_AUTOUIC ON)

# Setup for shared library creation
set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS ON)
if(WIN32)
    set(CMAKE_SHARED_LIBRARY_PREFIX "")
endif()

find_package(Qt6 REQUIRED COMPONENTS Core Core5Compat)

set(SOURCES
    serialization.h
    transfer.h
    inbound.cpp
    outbound.cpp
    ss.cpp
    ssd.cpp
    trojan.cpp
    vless.cpp
    vmess.cpp
    vmess_new.cpp
)

add_library(${PROJECT_NAME} SHARED ${SOURCES})

target_include_directories(${PROJECT_NAME} 
    PUBLIC 
        ${CMAKE_CURRENT_SOURCE_DIR}
        ${CMAKE_CURRENT_SOURCE_DIR}/3rd/QJsonStruct
)

target_link_libraries(${PROJECT_NAME} 
    PRIVATE 
        Qt6::Core
        Qt6::Core5Compat
)