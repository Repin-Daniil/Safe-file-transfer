cmake_minimum_required(VERSION 3.11)

project(safe_tunnel CXX)
set(CMAKE_CXX_STANDARD 20)

include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
conan_basic_setup()

find_package(Boost 1.78.0 REQUIRED)
if (Boost_FOUND)
    include_directories(${Boost_INCLUDE_DIRS})
endif ()


set(THREADS_PREFER_PTHREAD_FLAG ON)

find_package(Threads REQUIRED)
find_package(OpenSSL REQUIRED)

add_executable(safe_tunnel src/main.cpp
        src/Application/Application.h
        src/Network/Server.h
        src/Network/Client.h

        src/Application/Application.cpp
        src/Network/Client.cpp
        src/Network/Server.cpp)

target_link_libraries(safe_tunnel PRIVATE Threads::Threads
        OpenSSL::SSL
        OpenSSL::Crypto)