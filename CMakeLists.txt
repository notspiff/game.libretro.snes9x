project(gameclient.snes9x)

cmake_minimum_required(VERSION 2.6)

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR})

enable_language(CXX)

find_package(xbmc REQUIRED)

include(ExternalProject)

externalproject_add(snes9x
                    GIT_REPOSITORY https://github.com/snes9xgit/snes9x
                    GIT_TAG 25c0e7c
                    PREFIX snes9x
                    CONFIGURE_COMMAND ""
                    INSTALL_COMMAND ""
                    BUILD_COMMAND make -C libretro
                    BUILD_IN_SOURCE 1)

set(SNES9X_CUSTOM_BINARY ${PROJECT_BINARY_DIR}/snes9x/src/snes9x/libretro/snes9x_libretro${CMAKE_SHARED_LIBRARY_SUFFIX}
                        snes9x_libretro${CMAKE_SHARED_LIBRARY_SUFFIX} snes9x)

build_addon(gameclient.snes9x SNES9X DEPLIBS)
add_dependencies(gameclient.snes9x snes9x)
