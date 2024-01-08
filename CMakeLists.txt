cmake_minimum_required(VERSION 3.22.1)
project("MSDFGen")

#Copy Runtime Config File
set(CURRENT_DIR ${CMAKE_CURRENT_SOURCE_DIR})


#build freetype lib
set(FREETYPE_INCLUDE_DIRS "")
list(APPEND FREETYPE_INCLUDE_DIRS ${CURRENT_DIR}/freetype/include)
file(GLOB_RECURSE FILES_FREETYPE "${CURRENT_DIR}/freetype/include/**.h" "${CURRENT_DIR}/freetype/src/**.c")
add_library(
   "freetype"
   ${FILES_FREETYPE}
)
target_include_directories(
    "freetype"
    PUBLIC
    ${FREETYPE_INCLUDE_DIRS}
)

#build msdfgen lib
set(MSDFGEN_INCLUDE_DIRS "")
list(APPEND MSDFGEN_INCLUDE_DIRS ${CURRENT_DIR}/freetype/include)
list(APPEND MSDFGEN_INCLUDE_DIRS ${CURRENT_DIR}/include)
file(GLOB_RECURSE FILES_MSDFGEN "${CURRENT_DIR}/include/**.h"
        "${CURRENT_DIR}/core/**.h"
        "${CURRENT_DIR}/core/**.hpp"
        "${CURRENT_DIR}/core/**.cpp"
        "${CURRENT_DIR}/ext/**.h"
        "${CURRENT_DIR}/ext/**.hpp"
        "${CURRENT_DIR}/ext/**.cpp"
        "${CURRENT_DIR}/lib/**.cpp")
add_library(
        "msdfgen"
        ${FILES_MSDFGEN}
)
target_include_directories(
        "msdfgen"
        PUBLIC
        ${MSDFGEN_INCLUDE_DIRS}
)
target_link_libraries("msdfgen" freetype)