cmake_minimum_required(VERSION 3.30...4.2)

project(hash-library
    HOMEPAGE_URL "https://github.com/stbrumme/hash-library"
    DESCRIPTION
    "Portable C++ hashing library"
    LANGUAGES CXX C
)
set(CMAKE_CXX_SCAN_FOR_MODULES OFF)

option(BUILD_SHARED_LIBS "Build shared libraries" OFF)
option(hash-library_BUILD_SHARED_LIB "Build a shared version of hash-library" ${BUILD_SHARED_LIBS})

set(HASH_LIBRARY_SRC
    crc32.cpp
    digest.cpp
    keccak.cpp
    md5.cpp
    sha1.cpp
    sha256.cpp
    sha3.cpp
)
list(TRANSFORM HASH_LIBRARY_SRC PREPEND ${CMAKE_CURRENT_SOURCE_DIR}/src/)


if(hash-library_BUILD_SHARED_LIB)
    add_library(hash-library SHARED)
else()
    add_library(hash-library STATIC)
endif()
add_library(hash-library::hash-library ALIAS hash-library)

target_sources(hash-library PRIVATE ${HASH_LIBRARY_SRC})
target_sources(hash-library
    PUBLIC
    FILE_SET pub_headers
    TYPE HEADERS
    BASE_DIRS
    include/)

target_compile_features(hash-library PRIVATE cxx_std_23)