cmake_minimum_required(VERSION 3.15)

PROJECT("paraview-filter")
include(ExternalProject)

string(REPLACE "package" "build" ParaView_DIR ${CONAN_PARAVIEW_ROOT})
message(STATUS "Using conan Paraview dir: ${ParaView_DIR}")
ExternalProject_Add(
    vtk-timefilter
    GIT_REPOSITORY https://github.com/Chrismarsh/vtk-paraview-datetimefilter.git

    CMAKE_ARGS  -DCMAKE_INSTALL_PREFIX=${CMAKE_BINARY_DIR}
                -DParaView_DIR=${ParaView_DIR}
                -DCMAKE_TOOLCHAIN_FILE=${CMAKE_TOOLCHAIN_FILE}
    UPDATE_COMMAND ""
    BUILD_COMMAND make -j${EXTERNAL_BUILD_THREADS}
    INSTALL_COMMAND make install
    BUILD_IN_SOURCE 1
 )
