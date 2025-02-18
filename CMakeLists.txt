
cmake_minimum_required(VERSION 3.21)

project(dmmarkdown C CXX)

LIST(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake)
INCLUDE(cmake/ModuleImport.cmake)
INCLUDE(cmake/ModuleCompileOptions.cmake)
ModuleSetCompileOptions()
ModuleSetWinCompilerFlags()

set(MD_VERSION_MAJOR 0)
set(MD_VERSION_MINOR 5)
set(MD_VERSION_RELEASE 2)
set(MD_VERSION "${MD_VERSION_MAJOR}.${MD_VERSION_MINOR}.${MD_VERSION_RELEASE}")

set(PROJECT_VERSION "${MD_VERSION}")
set(PROJECT_URL "https://github.com/mity/md4c")

ADD_DEFINITIONS(-DMD4C_USE_UTF8 -DMD_VERSION_MAJOR=${MD_VERSION_MAJOR} -DMD_VERSION_MINOR=${MD_VERSION_MINOR} -DMD_VERSION_RELEASE=${MD_VERSION_RELEASE})

LibImport("md4c" "src/md4c")

IF (PROJECT_IS_TOP_LEVEL)
    ExeImport("tools" "md4c")
    
    AddInstall(md2html)
ENDIF()
