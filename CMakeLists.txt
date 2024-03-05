cmake_minimum_required(VERSION 2.8)
project(METIS C)

set(SHARED FALSE CACHE BOOL "build a shared library")

option(METIS_SHARED "Build shared library" ${SHARED})
option(METIS_INSTALL "Install METIS" FALSE)

# METIS' custom options
option(IDX64 "enable 64 bit ints" OFF)
option(REAL64 "enable 64 bit floats (i.e., double)" OFF)

# Configure libmetis library.
if(METIS_SHARED)
    set(SHARED ON)
else()
    set(SHARED OFF)
endif(METIS_SHARED)

if(SHARED)
    set(METIS_LIBRARY_TYPE SHARED)
else()
    set(METIS_LIBRARY_TYPE STATIC)
endif(SHARED)

include(./conf/gkbuild.cmake)

if(IDX64)
    set(METIS_IDX_BITS 64)
else()
    set(METIS_IDX_BITS 32)
endif(IDX64)

if(REAL64)
    set(METIS_REAL_BITS 64)
else()
    set(METIS_REAL_BITS 32)
endif(REAL64)

# Add include directories.
# i.e., the -I equivalent
# include_directories(build/xinclude)
# include_directories(${GKLIB_PATH}/include)
# include_directories(${CMAKE_INSTALL_PREFIX}/include)

# List of paths that the compiler will search for library files.
# i.e., the -L equivalent
# link_directories(${GKLIB_PATH}/lib)
# link_directories(${CMAKE_INSTALL_PREFIX}/lib)

# Recursively look for CMakeLists.txt in subdirs.
# add_subdirectory("build/xinclude")
add_subdirectory("libmetis")
add_subdirectory("programs")
