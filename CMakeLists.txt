project(f2c)
cmake_minimum_required(VERSION 3.1)

include (CheckFunctionExists)
include (CheckTypeSize)
check_function_exists( atexit HAVE_ATEXIT )
check_function_exists( fseeko HAVE_FSEEKO )
check_function_exists( ftruncate HAVE_FTRUNCATE )
check_function_exists( isatty HAVE_ISATTY )
check_function_exists( mkdtemp HAVE_MKDTEMP )
check_function_exists( onexit HAVE_ONEXIT )
check_function_exists( tmpfile HAVE_TMPFILE )

set(PACKAGE "f2c")
set(PACKAGE_BUGREPORT "jjgarcia@users.sourceforge.net")
set(PACKAGE_NAME "F2C Fortran to C99 compiler")
set(PACKAGE_STRING "F2C Fortran to C99 compiler 12.02.01")
set(PACKAGE_TARNAME "f2c")
set(PACKAGE_URL "")
set(PACKAGE_VERSION "12.02.01")
set(VERSION "12.02.01")

configure_file ("${PROJECT_SOURCE_DIR}/config_aux/config_cmake.h.in"
                "${PROJECT_BINARY_DIR}/config.h" )

check_type_size(long F2C_INT_BYTES)
math(EXPR F2C_INT_BITS 8*${F2C_INT_BYTES})
check_type_size(long F2C_LONG_BYTES)
math(EXPR F2C_LONG_BITS 8*${F2C_LONG_BYTES})
check_type_size(long F2C_LONG_LONG_BYTES)
math(EXPR F2C_LONG_LONG_BITS 8*${F2C_LONG_LONG_BYTES})

configure_file ("${PROJECT_SOURCE_DIR}/include/f2c_types_cmake.h.in"
                "${PROJECT_BINARY_DIR}/f2c_types.h" )

set(F2C_INSTALL_DIR_BIN bin CACHE STRING "runtime install dir")
set(F2C_INSTALL_DIR_LIB lib CACHE STRING "lib install dir")
set(F2C_INSTALL_DIR_INCLUDE include CACHE STRING "include install dir")
set(F2C_INSTALL_DIR RUNTIME DESTINATION ${F2C_INSTALL_DIR_BIN} LIBRARY DESTINATION ${F2C_INSTALL_DIR_LIB} ARCHIVE DESTINATION ${F2C_INSTALL_DIR_LIB})

include_directories(${PROJECT_BINARY_DIR})
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)
add_subdirectory(lib)
add_subdirectory(src)
add_subdirectory(include)
