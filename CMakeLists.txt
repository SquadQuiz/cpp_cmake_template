# Setup Cmake Version
cmake_minimum_required(VERSION 3.25)

# Setup compiler settings
set(CMAKE_CXX_STANDARD              17)
set(CMAKE_CXX_STANDARD_REQUIRED     ON)
set(CMAKE_CXX_EXTENSIONS            ON) 
# Setup Project Path
set(PROJ_PATH                       ${CMAKE_CURRENT_SOURCE_DIR}) 

#
# Core project settings
#
project(PROJECT_NAME_HERE)
enable_language(C CXX ASM)
set(EXECUTABLE                      ${CMAKE_PROJECT_NAME})

#
# List of source files to compile
#
set(SOURCES_SRCS
  # Put here your source files, one in each line, relative to CMakeLists.txt file location
  # Core Source files
  ${PROJ_PATH}/src/main.cpp

)

#
# Include directories
#
set(INCLUDE_PATH
  # Put here your include dirs, one in each line, relative to CMakeLists.txt file location
  ${PROJ_PATH}/inc/
)

# Executable files
add_executable(${EXECUTABLE} ${SOURCES_SRCS})

# Include paths
target_include_directories(${EXECUTABLE} PUBLIC  ${INCLUDE_PATH})

# Compiler options
target_compile_options(${EXECUTABLE} PUBLIC 
  -Wall
  -fdiagnostics-color=always
)

# Execute post-build to print size
add_custom_command(TARGET ${EXECUTABLE} POST_BUILD
  COMMAND ${CMAKE_SIZE} $<TARGET_FILE:${EXECUTABLE}>
)