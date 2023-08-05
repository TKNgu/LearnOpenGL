#Cmake version.
cmake_minimum_required(VERSION 3.10.2)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
include(ExternalProject)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_EXE_LINKER_FLAGS "-no-pie")

# Project
project(LearnOpenGL VERSION 1.0.0 LANGUAGES CXX C DESCRIPTION "Learn OpenGL")
option(BUILD_DEBUG "Build Debug" ON)
if(BUILD_DEBUG)
    add_definitions(-DDEBUG)
endif(BUILD_DEBUG)

# # OpenSSL
# set(OPENSSL_ROOT_DIR ${CMAKE_SOURCE_DIR}/lib/local/)
# find_package(OpenSSL 3.1.0)
# if(NOT OPENSSL_FOUND)
#     ExternalProject_Add(libopenssl
#         GIT_REPOSITORY https://github.com/openssl/openssl.git
#         GIT_TAG openssl-3.1.0
#         PREFIX ${CMAKE_SOURCE_DIR}/lib/libopenssl/
#         CONFIGURE_COMMAND ${CMAKE_SOURCE_DIR}/lib/libopenssl/src/libopenssl/Configure
#             --prefix=${CMAKE_SOURCE_DIR}/lib/local/
#         BUILD_COMMAND ${MAKE}
#         INSTALL_COMMAND make install)
# endif()
#
# # Libevent
# find_package(Libevent 2.1.12 HINTS ${CMAKE_SOURCE_DIR}/lib/local/)
# if(NOT Libevent_FOUND)
#     ExternalProject_Add(libevent
#         GIT_REPOSITORY https://github.com/libevent/libevent.git
#         GIT_TAG release-2.1.12-stable
#         PREFIX ${CMAKE_SOURCE_DIR}/lib/libevent/
#         CMAKE_ARGS
# 	        -DCMAKE_INSTALL_PREFIX:PATH=${CMAKE_SOURCE_DIR}/lib/local/
#     )
#     if(NOT OPENSSL_FOUND)
#         add_dependencies(libevent libopenssl)
#     endif()
# endif()
#
# # Curl
# find_package(CURL 8.0.1 HINTS ${CMAKE_SOURCE_DIR}/lib/local/)
# if(NOT CURL_FOUND)
#     ExternalProject_Add(libcurl
#         GIT_REPOSITORY https://github.com/curl/curl.git
#         GIT_TAG curl-8_0_1
#         PREFIX ${CMAKE_SOURCE_DIR}/lib/curl/
#         CMAKE_ARGS
#             -DCURL_ENABLE_SSL=ON -DCURL_USE_OPENSSL=ON
#     		-DCMAKE_INSTALL_PREFIX:PATH=${CMAKE_SOURCE_DIR}/lib/local/)
#     if(NOT OPENSSL_FOUND)
#         add_dependencies(libcurl libopenssl)
#     endif()
# endif()
#
# # Sqlite3
# set(CMAKE_PREFIX_PATH "${CMAKE_SOURCE_DIR}/lib/local/")
# pkg_search_module(SQLite3 sqlite3)
# if(NOT SQLite3_FOUND)
#     ExternalProject_Add(libsqlite3
#         GIT_REPOSITORY https://github.com/sqlite/sqlite.git
#         GIT_TAG version-3.41.2
#         PREFIX ${CMAKE_SOURCE_DIR}/lib/sqlite3/
#         CONFIGURE_COMMAND ${CMAKE_SOURCE_DIR}/lib/sqlite3/src/libsqlite3/configure
#             --prefix=${CMAKE_SOURCE_DIR}/lib/local/
#         BUILD_COMMAND $(MAKE)
#         INSTALL_COMMAND make install)
# endif()
#
# # Json
# find_package(nlohmann_json 3.11.2 HINTS ${CMAKE_SOURCE_DIR}/lib/local/)
# if(NOT nlohmann_json_FOUND)
#     ExternalProject_Add(nlohmann_json
#         GIT_REPOSITORY https://github.com/nlohmann/json.git
#         GIT_TAG v3.11.2
#         PREFIX ${CMAKE_SOURCE_DIR}/lib/nlohmann_json/
#         CMAKE_ARGS
# 		   -DCMAKE_INSTALL_PREFIX:PATH=${CMAKE_SOURCE_DIR}/lib/local/)
# endif()

include_directories(
    ${CMAKE_SOURCE_DIR}/lib/local/include)

link_directories(
    ${CMAKE_SOURCE_DIR}/lib/local/lib
    ${CMAKE_SOURCE_DIR}/lib/local/lib64)

file(GLOB SRC
    src/*.cpp)

add_executable(${CMAKE_PROJECT_NAME} ${SRC})
target_link_libraries(${CMAKE_PROJECT_NAME}) 
add_custom_target(run ${CMAKE_PROJECT_NAME}
    DEPENDS ${SAMPLE}
    WORKING_DIRECTORY ${PROJECT_SOURCE_DIR})
