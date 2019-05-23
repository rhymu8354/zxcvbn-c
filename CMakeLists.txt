# CMakeLists.txt for zxcvbn
#
# © 2019 by Richard Walters

cmake_minimum_required(VERSION 3.8)
set(This zxcvbn)

set(dict-src ${CMAKE_CURRENT_BINARY_DIR}/dict-src.h)

set(Headers
    zxcvbn.h
    ${dict-src}
)

set(Sources
    zxcvbn.c
)

set(Words
    ${CMAKE_CURRENT_SOURCE_DIR}/words-eng_wiki.txt
    ${CMAKE_CURRENT_SOURCE_DIR}/words-female.txt
    ${CMAKE_CURRENT_SOURCE_DIR}/words-male.txt
    ${CMAKE_CURRENT_SOURCE_DIR}/words-passwd.txt
    ${CMAKE_CURRENT_SOURCE_DIR}/words-surname.txt
    ${CMAKE_CURRENT_SOURCE_DIR}/words-tv_film.txt
)

add_executable(dictgen dict-generate.cpp)

add_custom_command(
    OUTPUT ${dict-src}
    DEPENDS dictgen
    COMMAND $<TARGET_FILE:dictgen> -o ${dict-src} ${Words}
)

add_library(${This} STATIC ${Sources} ${Headers})
set_target_properties(${This} PROPERTIES
    FOLDER Libraries
)

target_include_directories(${This} PUBLIC .)
target_include_directories(${This} PRIVATE ${CMAKE_CURRENT_BINARY_DIR})

target_link_libraries(${This} PUBLIC
)
