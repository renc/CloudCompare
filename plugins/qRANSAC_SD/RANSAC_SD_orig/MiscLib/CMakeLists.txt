cmake_minimum_required(VERSION 2.8)

include_directories( ${CMAKE_CURRENT_SOURCE_DIR} )

project( QRANSAC_SD_MISC_LIB )

file( GLOB header_list *.h )
file( GLOB source_list *.cpp )

# renc 
SET( CMAKE_ARCHIVE_OUTPUT_DIRECTORY_DEBUG	"${CMAKE_BINARY_DIR}/bin/Debug")
SET( CMAKE_ARCHIVE_OUTPUT_DIRECTORY_RELEASE "${CMAKE_BINARY_DIR}/bin/Release")
SET( CMAKE_RUNTIME_OUTPUT_DIRECTORY_DEBUG	"${CMAKE_BINARY_DIR}/bin/Debug" )
SET( CMAKE_RUNTIME_OUTPUT_DIRECTORY_RELEASE "${CMAKE_BINARY_DIR}/bin/Release")


add_library( ${PROJECT_NAME} STATIC ${header_list} ${source_list} )

# Add preprocessor definitions
set_property( TARGET ${PROJECT_NAME} APPEND PROPERTY COMPILE_DEFINITIONS _CRT_SECURE_NO_DEPRECATE _CRT_SECURE_NO_WARNINGS )

if (OPENMP_FOUND AND NOT WIN32) #DGM: OpenMP doesn't work with Visual at least (the process loops infinitely)
	#set_property( TARGET ${PROJECT_NAME} APPEND PROPERTY COMPILE_DEFINITIONS DOPARALLEL )
endif()
