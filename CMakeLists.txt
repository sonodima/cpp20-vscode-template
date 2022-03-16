cmake_minimum_required(VERSION 3.20)
project(Build VERSION 0.1.0)
set(PROJECT_NAME cpp20-vscode-template)


# Main project directories
set(SRCS_DIR "${PROJECT_SOURCE_DIR}/src")
set(DEPS_DIR "${PROJECT_SOURCE_DIR}/deps")
set(OUT_DIR "${PROJECT_SOURCE_DIR}/out")

# Specify target executable output directory
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${OUT_DIR})
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${OUT_DIR})
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${OUT_DIR})


# Obtain all source files from the "src" directory
file(GLOB_RECURSE SRCS CONFIGURE_DEPENDS
  "${SRCS_DIR}/*.cc"
  "${SRCS_DIR}/*.cpp")
# Add source files to the target
add_executable(Build ${SRCS})


if(MSVC)
  target_compile_options(Build PRIVATE /W4 /WX)
else()
  target_compile_options(Build PRIVATE -Wall -Wextra -Wpedantic -Werror)
endif()


set_target_properties(Build PROPERTIES
  OUTPUT_NAME ${PROJECT_NAME}
  CXX_STANDARD 20
  CXX_STANDARD_REQUIRED ON)


set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})


include(CPack)
