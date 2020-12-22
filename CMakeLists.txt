cmake_minimum_required(VERSION 3.14)

project(md5)

add_library(md5 STATIC md5.cpp md5.h)
add_library(md5::md5 ALIAS md5)

target_include_directories(md5 INTERFACE $<INSTALL_INTERFACE:include>)

install(
    FILES md5.h
    DESTINATION include
)

install(
    FILES LICENSE
    DESTINATION share/md5
    RENAME copyright 
)

# install config file
configure_file(
    "${CMAKE_CURRENT_LIST_DIR}/md5-config.in.cmake"
    "${PROJECT_BINARY_DIR}/md5-config.cmake"
    @ONLY
)

install(
    FILES "${PROJECT_BINARY_DIR}/md5-config.cmake"
    DESTINATION share/md5
)

# install targets
install(
    TARGETS md5
    EXPORT md5-targets
    LIBRARY DESTINATION lib
)

install(EXPORT md5-targets 
    NAMESPACE md5::
    FILE md5-targets.cmake 
    DESTINATION share/md5
)