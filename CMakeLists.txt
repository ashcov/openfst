project(openfst)
include(CTest)
find_package(ICU COMPONENTS data i18n io  test tu uc)
if (ICU_FOUND)
  include_directories(${ICU_INCLUDE_DIRS})
  set(LIBS ${LIBS} ${ICU_LIBRARIES})
endif (ICU_FOUND)

find_package(ZLIB)
if (ZLIB_FOUND) 
  include_directories(${ZLIB_INCLUDE_DIRECTORIES})
  set(ZLIBS ${ZLIB_LIBRARIES})
endif (ZLIB_FOUND)

cmake_minimum_required(VERSION 3.1)
set(CMAKE_MACOSX_RPATH 1)
set(CMAKE_CXX_STANDARD 11)

if (WIN32)
  add_definitions(/bigobj)
  #set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS 1)
  #this must be disabled unless the previous option (CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS) is enabled
  option(BUILD_SHARED_LIBS "Build shared libraries" OFF)
else()
  option(BUILD_SHARED_LIBS "Build shared libraries" ON)
endif (WIN32)


OPTION(BUILD_USE_SOLUTION_FOLDERS "Enable grouping of projects in VS" ON) 
SET_PROPERTY(GLOBAL PROPERTY USE_FOLDERS ${BUILD_USE_SOLUTION_FOLDERS}) 


option(HAVE_BIN          "Build the fst binaries" ON)
option(HAVE_SCRIPT       "Build the fstscript" ON)
option(HAVE_COMPACT      "Build compact" ON)
option(HAVE_COMPRESS "Build compress" OFF)
option(HAVE_CONST   "Build const" ON)
option(HAVE_FAR  "Build far" ON)
option(HAVE_GRM "Build grm" ON)
option(HAVE_PDT "Build pdt" ON)
option(HAVE_MPDT "Build mpdt" ON)
option(HAVE_LINEAR "Build linear" ON)
option(HAVE_LOOKAHEAD "Build lookahead" ON)
option(HAVE_NGRAM "Build ngram" ON)
option(HAVE_PYTHON "Build python" OFF)
option(HAVE_SPECIAL "Build special" ON)

add_subdirectory(src)

