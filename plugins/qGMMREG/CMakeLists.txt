cmake_minimum_required(VERSION 3.0)


# renc 
SET( CMAKE_ARCHIVE_OUTPUT_DIRECTORY_DEBUG	"${CMAKE_BINARY_DIR}/bin/Debug")
SET( CMAKE_ARCHIVE_OUTPUT_DIRECTORY_RELEASE "${CMAKE_BINARY_DIR}/bin/Release")
SET( CMAKE_RUNTIME_OUTPUT_DIRECTORY_DEBUG	"${CMAKE_BINARY_DIR}/bin/Debug" )
SET( CMAKE_RUNTIME_OUTPUT_DIRECTORY_RELEASE "${CMAKE_BINARY_DIR}/bin/Release")

option( INSTALL_QGMMREG_PLUGIN "Check to install qGMMREG plugin" OFF )

# CloudCompare 'GMMREG' plugin
if (INSTALL_QGMMREG_PLUGIN)
	project( QGMMREG_PLUGIN )
	
	#As we are going to re-use several components of the main qCC project
	#we define its sources path relatively to the plugin's dir
	set(CloudCompare_SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/../../qCC)
	#find_package(VXL) # renc
	
	# Whether FIND_PACKAGE(VXL) worked is stored in the variable
	# VXL_FOUND.  If VXL was found we then include `UseVXL.cmake'
	# which will set many variables prefixed with VXL_ that your project
	# can use to determine what parts of VXL are present and how to use
	# them.  `UseVXL.cmake' holds all the necessary definitions that
	# CMake needs to use VXL.
	
	#if (VXL_FOUND)
	#	include(${VXL_CMAKE_DIR}/UseVXL.cmake)
	#else()
	#	message( SEND_ERROR "VXL is required to compile qGMMReg (VXL_DIR)" )
	#endif()
	include_directories(${CMAKE_SOURCE_DIR}/3rdLibraries/vxl/core) #renc
	include_directories(${CMAKE_SOURCE_DIR}/3rdLibraries/vxl/vcl) #renc 
	include_directories(D:/Users/renc/Source/Repos/vxl_build/vcl) #renc 
	include_directories(D:/Users/renc/Source/Repos/vxl_build/core) #renc 
	
	
	#load necessary libraries (see qPCV for an example)
	add_subdirectory (GMMREG/C++)
	
	#we need the 'order choice' dialog
	file( GLOB CC_PLUGIN_CUSTOM_HEADER_LIST ${CloudCompare_SOURCE_DIR}/ccOrderChoiceDlg*.h )
	file( GLOB CC_PLUGIN_CUSTOM_SOURCE_LIST ${CloudCompare_SOURCE_DIR}/ccOrderChoiceDlg*.cpp )
	set( CC_PLUGIN_CUSTOM_UI_LIST           ${CloudCompare_SOURCE_DIR}/ui_templates/roleChoiceDlg.ui )
	
	#if the plugin is an 'OpenGL filter', uncomment the line below
	#set( CC_OPENGL_FILTER ON BOOL)
	include( ../CMakePluginTpl.cmake )
	
	#set dependencies to necessary libraries (see qPCV for an example)
	include_directories( ${CloudCompare_SOURCE_DIR} )
	include_directories( ${GMMREG_LIB_SOURCE_DIR} )
	
	target_link_libraries( ${PROJECT_NAME} GMMREG_LIB )
	##target_link_libraries(${PROJECT_NAME} vnl_algo vnl vcl) # renc 
target_link_libraries(${PROJECT_NAME} 
		debug D:/Users/renc/Source/Repos/vxl_build/lib/Debug/vnl_algo.lib
		debug D:/Users/renc/Source/Repos/vxl_build/lib/Debug/vnl.lib 
		debug D:/Users/renc/Source/Repos/vxl_build/lib/Debug/vcl.lib 
		debug D:/Users/renc/Source/Repos/vxl_build/lib/Debug/v3p_netlib.lib 
		debug D:/Users/renc/Source/Repos/vxl_build/lib/Debug/vpl.lib 
		optimized D:/Users/renc/Source/Repos/vxl_build/lib/Release/vnl_algo.lib 
		optimized D:/Users/renc/Source/Repos/vxl_build/lib/Release/vnl.lib 
		optimized D:/Users/renc/Source/Repos/vxl_build/lib/Release/vcl.lib  
		optimized D:/Users/renc/Source/Repos/vxl_build/lib/Release/v3p_netlib.lib  
		optimized D:/Users/renc/Source/Repos/vxl_build/lib/Release/vpl.lib  	
	)
	if (UNIX)
	  target_link_libraries(${PROJECT_NAME} m port_ini)
	endif (UNIX)
endif()
