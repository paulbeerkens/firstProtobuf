cmake_minimum_required(VERSION 3.8)
project(protobufTest)

set(CMAKE_CXX_STANDARD 14)

#set up protobuf to be included
find_package(Protobuf REQUIRED)

#add all the protobuf directories
include_directories(${PROTOBUF_INCLUDE_DIRS}) #not needed if in /usr/include

include_directories(${CMAKE_CURRENT_BINARY_DIR}) #not needed if in /usr/lib

#This sets everything up for the proto files to be compiled. Will not do anything until the ${PROTO_SRCS} and ${PROTO_HDRS} are used as a target!
PROTOBUF_GENERATE_CPP(PROTO_SRCS PROTO_HDRS addressbook.proto)

message (STATUS ${PROTO_SRCS})

set(SOURCE_FILES main.cpp ${PROTO_SRCS} ${PROTO_HDRS})
add_executable(protobufTest ${SOURCE_FILES})

#link in the protobuf libraries
target_link_libraries(protobufTest ${PROTOBUF_LIBRARIES})