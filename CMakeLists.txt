project(game.libretro.snes9x)

cmake_minimum_required(VERSION 2.6)

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR})

enable_language(CXX)

find_package(kodi REQUIRED)
find_package(libretro-snes9x REQUIRED)

set(DEPLIBS snes9x)
set(SNES9X_CUSTOM_BINARY ${SNES9X_LIB}
                         ${PROJECT_NAME}${CMAKE_SHARED_LIBRARY_SUFFIX} snes9x)

build_addon(${PROJECT_NAME} SNES9X DEPLIBS)

