project(game.libretro.snes9x)

cmake_minimum_required(VERSION 2.6)

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR})

enable_language(CXX)

find_package(kodi REQUIRED)

if(CMAKE_BUILD_TYPE MATCHES Debug)
  set(LIBRETRO_DEBUG DEBUG=1)
endif()

if("${CORE_SYSTEM_NAME}" STREQUAL "windows")
  set(BUILD_COMMAND mingw32-make -C libretro platform=win ${LIBRETRO_DEBUG})
elseif("${CORE_SYSTEM_NAME}" STREQUAL "linux")
  set(BUILD_COMMAND make -C libretro ${LIBRETRO_DEBUG})
elseif("${CORE_SYSTEM_NAME}" STREQUAL "darwin")
  set(BUILD_COMMAND make -C libretro platform=osx ${LIBRETRO_DEBUG})
elseif("${CORE_SYSTEM_NAME}" STREQUAL "ios")
  # TODO
elseif("${CORE_SYSTEM_NAME}" STREQUAL "android")
  # TODO
elseif("${CORE_SYSTEM_NAME}" STREQUAL "rbpi")
  # TODO
elseif("${CORE_SYSTEM_NAME}" STREQUAL "freebsd")
# TODO
endif()

include(ExternalProject)
externalproject_add(snes9x
                    GIT_REPOSITORY https://github.com/snes9xgit/snes9x
                    GIT_TAG 25c0e7c
                    PREFIX snes9x
                    CONFIGURE_COMMAND ""
                    INSTALL_COMMAND ""
                    BUILD_COMMAND ${BUILD_COMMAND}
                    BUILD_IN_SOURCE 1)

set(SNES9X_CUSTOM_BINARY ${PROJECT_BINARY_DIR}/snes9x/src/snes9x/libretro/snes9x_libretro${CMAKE_SHARED_LIBRARY_SUFFIX}
                         game.libretro.snes9x${CMAKE_SHARED_LIBRARY_SUFFIX} snes9x)

build_addon(game.libretro.snes9x SNES9X DEPLIBS)
add_dependencies(game.libretro.snes9x snes9x)

include(CPack)
