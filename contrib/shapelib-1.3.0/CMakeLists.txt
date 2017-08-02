cmake_minimum_required(VERSION 3.0)

project( SHAPELIB )

# renc 
SET( CMAKE_ARCHIVE_OUTPUT_DIRECTORY_DEBUG	"${CMAKE_BINARY_DIR}/bin/Debug")
SET( CMAKE_ARCHIVE_OUTPUT_DIRECTORY_RELEASE "${CMAKE_BINARY_DIR}/bin/Release")
SET( CMAKE_RUNTIME_OUTPUT_DIRECTORY_DEBUG	"${CMAKE_BINARY_DIR}/bin/Debug" )
SET( CMAKE_RUNTIME_OUTPUT_DIRECTORY_RELEASE "${CMAKE_BINARY_DIR}/bin/Release")


set( CMAKE_AUTOMOC OFF )

file( GLOB header_list *.h )
file( GLOB source_list *.c )


add_library( ${PROJECT_NAME} STATIC ${header_list} ${source_list} )