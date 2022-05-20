cmake_minimum_required(VERSION 3.14 FATAL_ERROR)

project(UANTLR VERSION 0.3.0)
message(STATUS "[Project] ${PROJECT_NAME}")

include(cmake/InitUCMake.cmake)
Ubpa_InitUCMake(VERSION 0.6.4)

Ubpa_InitProject()

Ubpa_DownloadZip(
  https://github.com/WangZhihua1998/UANTLR/releases/download/0.3.0/antlr4_runtime_20220520.zip
  antlr4_runtime_20220520.zip
  SHA256 12ac31d961666db33463eb80a3c62838881e78aaa8fd0ff5539dbce48607c454
)

Ubpa_DownloadZip(
  https://github.com/WangZhihua1998/UANTLR/releases/download/0.3.0/antlr4_cpp14_20220520.zip
  antlr4_cpp14_20220520.zip
  SHA256 aa3d10ae27c937f5839b301a8e28953d299a4f0f653bcab0772304d6acd65fdd
)
# name in antlr4_cpp14_20201115.zip is wrong, so change it here
if(EXISTS "${PROJECT_SOURCE_DIR}/include/UANTLR/ParserCPP14")
  file(RENAME "${PROJECT_SOURCE_DIR}/include/UANTLR/ParserCPP14" "${PROJECT_SOURCE_DIR}/include/UANTLR/ParserCpp14")
endif()

Ubpa_AddSubDirsRec(include)
Ubpa_AddSubDirsRec(src)

Ubpa_PackageName(package_name)

Ubpa_Export(
  TARGET
  DIRECTORIES
    "include"
	  "cmake"
)
