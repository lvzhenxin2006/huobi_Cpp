cmake_minimum_required(VERSION 2.8)
set(platform x64)
PROJECT(unittest)

include_directories(../include)
include_directories(../3rdparty/gtest/include)
include_directories(../3rdparty/gmock/include)

AUX_SOURCE_DIRECTORY(. DIR_SRCS)

ADD_EXECUTABLE(${PROJECT_NAME} ${DIR_SRCS})

find_library(LIBGTEST_PATH gtest ../3rdparty/gtest/lib)
IF(NOT LIBGTEST_PATH)
MESSAGE(FATAL_ERROR "gtest not found")
ENDIF(NOT LIBGTEST_PATH)
MESSAGE(STATUS ${LIBGTEST_PATH} " found")

find_library(LIBGTEST_MAIN_PATH gtest_main ../3rdparty/gtest/lib)
IF(NOT LIBGTEST_MAIN_PATH)
MESSAGE(FATAL_ERROR "gtest main not found")
ENDIF(NOT LIBGTEST_MAIN_PATH)
MESSAGE(STATUS ${LIBGTEST_MAIN_PATH} " found")

find_library(LIBGMOCK_PATH gmock ../3rdparty/gmock/lib)
IF(NOT LIBGMOCK_PATH)
MESSAGE(FATAL_ERROR "gmock not found")
ENDIF(NOT LIBGMOCK_PATH)
MESSAGE(STATUS ${LIBGMOCK_PATH} " found")

find_library(LIBWEBSOCKET_PATH websockets ../3rdparty/libwebsockets/lib)
IF(NOT LIBWEBSOCKET_PATH)
MESSAGE(FATAL_ERROR "libwebsockets not found")
ENDIF(NOT LIBWEBSOCKET_PATH)
MESSAGE(STATUS ${LIBWEBSOCKET_PATH} " found")

find_library(LIBSSL_PATH ssl ../3rdparty/openssl/lib)
IF(NOT LIBSSL_PATH)
MESSAGE(FATAL_ERROR "libssl not found")
ENDIF(NOT LIBSSL_PATH) 
MESSAGE(STATUS ${LIBSSL_PATH} " found")

find_library(LIBCRYPTO_PATH crypto ../3rdparty/openssl/lib)
IF(NOT LIBCRYPTO_PATH)
MESSAGE(FATAL_ERROR "libcrypto not found")
ENDIF(NOT LIBCRYPTO_PATH) 
MESSAGE(STATUS ${LIBCRYPTO_PATH} " found")

find_library(LIBCURL_PATH curl ../3rdparty/curl/lib)
IF(NOT LIBCURL_PATH)
MESSAGE(FATAL_ERROR "curl not found")
ENDIF(NOT LIBCURL_PATH) 
MESSAGE(STATUS ${LIBCURL_PATH} " found")

find_library(LIBZ_PATH z ../3rdparty/zlib/lib)
IF(NOT LIBZ_PATH)
MESSAGE(FATAL_ERROR "z not found")
ENDIF(NOT LIBZ_PATH) 
MESSAGE(STATUS ${LIBZ_PATH} " found")

find_library(LIBDECNUMBER_PATH decnumber ../3rdparty/libdecnumber/lib)
IF(NOT LIBDECNUMBER_PATH)
MESSAGE(FATAL_ERROR "decnumber not found")
ENDIF(NOT LIBDECNUMBER_PATH) 
MESSAGE(STATUS ${LIBDECNUMBER_PATH} " found")

add_definitions(-std=c++11)

TARGET_LINK_LIBRARIES(${PROJECT_NAME} HuobiClient ${LIBDECNUMBER_PATH} ${LIBGTEST_PATH} ${LIBGTEST_MAIN_PATH} ${LIBGMOCK_PATH} ${LIBSSL_PATH} ${LIBCRYPTO_PATH} ${LIBWEBSOCKET_PATH} ${LIBCURL_PATH} ${LIBZ_PATH} pthread)
add_custom_command(TARGET ${PROJECT_NAME}
    POST_BUILD
    COMMAND ./unittest
)
