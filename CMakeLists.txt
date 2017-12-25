# CMake build file.

#
# To use this CMake file, execute (on the directory of CMakeLists.txt)
#
# $ mkdir build && cd build
# $ cmake .. -DCMAKE_BUILD_TYPE=Debug -DCMAKE_EXPORT_COMPILE_COMMANDS=ON
# $ mv compile_commands.json ../compile_commands.json
#
# It is recommended to create a separate directory (build) to store the
# intermediate objects for compilation.
#
# The argument -DCMAKE_BUILD_TYPE=Debug puts CMake in debug mode. Remove it to
# build in release mode.
#
# The argument -DCMAKE_EXPORT_COMPILE_COMMANDS=ON allows CMake to write the
# compile commands for each file in compile_commands.json. This can be used by
# some plugins (YouCompleteMe, for example) for syntax highlighting.
#

#
# To compile this project, execute the following in build/:
# $ make
#

# Sets the project name. This will be used as the name of the compiled
# executable.
project(CMin)

# Minimal version of CMake required
cmake_minimum_required(VERSION 3.5)

#
# Sets the directories.
#
# ${CMAKE_SOURCE_DIR} is the directory containing the CMakeLists.txt file.
#
# If ${CMAKE_SOURCE_DIR} is CMin/,
#
#    ${PROJECT_SOURCE_DIR} is CMin/src: Source files are located here.
#    ${CMAKE_BINARY_DIR} is CMin/bin: Binary files are located here.
#    ${EXECUTABLE_OUTPUT_PATH} is the location of the exported executables
#    ${LIBRARY_OUTPUT_PATH} is the location of the exported libraries.
#
set(PROJECT_SOURCE_DIR ${CMAKE_SOURCE_DIR}/src)
set(CMAKE_BINARY_DIR   ${CMAKE_SOURCE_DIR}/bin)
set(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR})
set(LIBRARY_OUTPUT_PATH    ${CMAKE_BINARY_DIR})

#
# Creates a variable StdFeatures. CMake will require the compiler to provide
# these features.
#
set(StdFeatures
	cxx_range_for
	cxx_noexcept
	cxx_rvalue_references
	cxx_override
	cxx_final
	cxx_deleted_functions
	cxx_delegating_constructors
	cxx_auto_type
	cxx_constexpr
	cxx_lambdas
	)

# The command message(...) outputs a message.

# Outputs all available StdFeatures for C and C++:
message("${CMAKE_C_COMPILE_FEATURES}")
message("${CMAKE_CXX_COMPILE_FEATURES}")

#
# [Optional]
# This loads the threading package.
#
# Notice that when this fails, CMake outputs an error.
#
find_package(Threads REQUIRED)

#
# Creates a variable that stores all the source file names.
# [C++] Uncomment src/main.cpp and comment src/main.c to switch to cpp mode.
set(FileSource
	src/main.c
	#src/main.cpp
	)

#
# Below we link the executable to the source files.
#
# The executable "CMin" is a "target" for CMake.
add_executable(CMin ${FileSource})
target_link_libraries(CMin ${CMAKE_THREAD_LIBS_INIT})
target_compile_features(CMin PRIVATE ${StdFeatures})

