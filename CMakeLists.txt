cmake_minimum_required(VERSION 3.30)

project(HASH-LIBRARY)

set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_SCAN_FOR_MODULES OFF)

set(HASH_LIBRARY_SRC
    crc32.cpp
    crc32.h
    digest.cpp
    hash.h
    hmac.h
    keccak.cpp
    keccak.h
    md5.cpp
    md5.h
    readme.md
    sha1.cpp
    sha1.h
    sha256.cpp
    sha256.h
    sha3.cpp
    sha3.h)
list(TRANSFORM HASH_LIBRARY_SRC PREPEND ${CMAKE_CURRENT_SOURCE_DIR}/)

add_library(hash-library SHARED ${HASH_LIBRARY_SRC})
add_library(hash-library::hash-library ALIAS hash-library)

target_include_directories(hash-library PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/)

