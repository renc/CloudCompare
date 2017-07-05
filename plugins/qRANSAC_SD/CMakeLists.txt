cmake_minimum_required(VERSION 3.0)

option( INSTALL_QRANSAC_SD_PLUGIN "Check to install qRansac_SD (Shape Detection) plugin" OFF )

# renc 
SET( CMAKE_ARCHIVE_OUTPUT_DIRECTORY_DEBUG	"${CMAKE_BINARY_DIR}/bin/Debug")
SET( CMAKE_ARCHIVE_OUTPUT_DIRECTORY_RELEASE "${CMAKE_BINARY_DIR}/bin/Release")
SET( CMAKE_RUNTIME_OUTPUT_DIRECTORY_DEBUG	"${CMAKE_BINARY_DIR}/bin/Debug" )
SET( CMAKE_RUNTIME_OUTPUT_DIRECTORY_RELEASE "${CMAKE_BINARY_DIR}/bin/Release")

# CloudCompare 'Ransac Shape Detection' plugin
if (INSTALL_QRANSAC_SD_PLUGIN)
	project( QRANSAC_SD_PLUGIN )

	add_subdirectory (RANSAC_SD_orig)

	include( ../CMakePluginTpl.cmake )

	target_link_libraries( ${PROJECT_NAME} QRANSAC_SD_PRIM_SHAPES_LIB QRANSAC_SD_MISC_LIB )

	include_directories( ${QRANSAC_SD_MISC_LIB_SOURCE_DIR} )
	include_directories( ${QRANSAC_SD_PRIM_SHAPES_LIB_SOURCE_DIR} )
	include_directories( ${QRANSAC_SD_PRIM_SHAPES_LIB_SOURCE_DIR}/GfxTL )

if (OPENMP_FOUND AND NOT WIN32) #DGM: OpenMP doesn't work with Visual at least (the process loops infinitely)
	set_property( TARGET ${PROJECT_NAME} APPEND PROPERTY COMPILE_DEFINITIONS DOPARALLEL )
endif()

endif()
