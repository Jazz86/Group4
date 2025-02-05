# Copyright (c) 2021, 鍾淯丞, 周杰仕, 林仁鴻. All rights reserved.
# Use of this source code is governed by a BSD-style license that can be
# found in the LICENSE file.

cmake_minimum_required(VERSION 3.10)
project(AllTest)
enable_testing()

file(MAKE_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/log)

set(EXECUTABLE_OUTPUT_PATH ${CMAKE_CURRENT_SOURCE_DIR}/build)
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/Modules/")

include_directories(${GMOCK_ROOT}/include)
include_directories(${GMOCK_ROOT}/gtest/include)
include_directories(${GTEST_INCLUDE_DIRS})
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/src/Header)
message(STATUS ${GMOCK_ROOT})
find_package(GTest REQUIRED)

include(GoogleTest)

set(BasicFile 
			src/Implement/Authenticator.cpp
			src/Implement/OperateData.cpp
			src/Implement/DownloadStream.cpp
			src/Implement/RequestHandler.cpp
			src/Implement/FileOperator.cpp
			src/Implement/RequestParser.cpp
			src/Implement/HttpListener.cpp
			src/Implement/ResponseEncoder.cpp
			src/Implement/LogHandle.cpp
			src/Implement/ResponseHandler.cpp
			src/Implement/MainManager.cpp
			src/Implement/UploadStream.cpp
			
			src/Header/APIHandler.h
			src/Header/FileOperator.h
			src/Header/MainManager.h
			src/Header/RequestParser.h
			src/Header/Authenticator.h
			src/Header/HttpListener.h
			src/Header/OperateData.h
			src/Header/ResponseEncoder.h
			src/Header/DownloadStream.h
			src/Header/LogHandle.h
			src/Header/RequestHandler.h
			src/Header/ResponseHandler.h
			src/Header/UploadStream.h
			)

if(UNIX)
add_executable(UnitTest 
# Made by younger15
#			src/Implement/UnitTestRequestHandler.cpp
#			src/Implement/UnitTestMainManager.cpp
#			src/Implement/UnitTestHttpListener.cpp
			# src/Implement/UnitTestRequestParser.cpp
			# src/Header/RequestParser.h
			# src/Implement/RequestParser.cpp
			# src/Header/OperateData.h
			# src/Implement/OperateData.cpp
#			src/Implement/UnitTestAuthenticator.cpp
# Made by Jazz
#			src/Implement/UnitTestOperateData.cpp
#			src/Implement/UnitTestErrorHandle.cpp
#			src/Implement/UnitTestDownloadStream.cpp
#			src/Implement/UnitTestUploadStream.cpp
# Made by Hong
#			src/Implement/UnitTestResponseParser.cpp
#			src/Implement/UnitTestResponseHandler.cpp
#			src/Implement/UnitTestResponseEncoder.cpp
#			src/Implement/UnitTestFileOperator.cpp
# All src			
#			src/Implement/RequestHandler.cpp
#			src/Header/RequestHandler.h
#			src/Implement/RequestParser.cpp
#			src/Header/RequestParser.h
#			src/Implement/OperateData.cpp
#			src/Header/OperateData.h
			${BasicFile}
			
			src/Implement/UnitTestMainManager.cpp
			src/Implement/UnitTestResponseHandler.cpp
			src/Implement/UnitTestDownloadStream.cpp
			src/Implement/UnitTestRequestHandler.cpp
			src/Implement/UnitTestRequestParser.cpp
			src/Implement/UnitTestFileOperator.cpp
			src/Implement/UnitTestResponseEncoder.cpp
			src/Implement/UnitTestLogHandle.cpp
			src/Implement/UnitTestOperateData.cpp
			src/Implement/UnitTestUploadStream.cpp
			src/Implement/UnitTestAuthenticator.cpp
			src/Implement/UnitTestHttpListener.cpp
			)

add_executable(Server 
			${BasicFile}
			src/main.cpp
			)

# command between 3.16 and 3.20 for gtest is different
if(CMAKE_MINOR_VERSION LESS 20})
	target_link_libraries(UnitTest pthread GTest::GTest GTest::Main)
	target_link_libraries(Server pthread GTest::GTest GTest::Main)
else()
	target_link_libraries(UnitTest pthread GTest::gtest GTest::gtest_main GTest::gmock GTest::gmock_main)
	target_link_libraries(Server pthread GTest::gtest GTest::gtest_main GTest::gmock GTest::gmock_main)
endif()
	gtest_discover_tests(UnitTest)
	add_test(UnitTest_test UnitTest)
else()
	message( FATAL_ERROR "must be Linux based OS")
endif()

