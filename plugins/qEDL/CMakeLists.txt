cmake_minimum_required(VERSION 3.0)



# renc 
SET( CMAKE_ARCHIVE_OUTPUT_DIRECTORY_DEBUG	"${CMAKE_BINARY_DIR}/bin/Debug")
SET( CMAKE_ARCHIVE_OUTPUT_DIRECTORY_RELEASE "${CMAKE_BINARY_DIR}/bin/Release")
SET( CMAKE_RUNTIME_OUTPUT_DIRECTORY_DEBUG	"${CMAKE_BINARY_DIR}/bin/Debug" )
SET( CMAKE_RUNTIME_OUTPUT_DIRECTORY_RELEASE "${CMAKE_BINARY_DIR}/bin/Release")


option( INSTALL_QEDL_PLUGIN "Check to install qEDL plugin" OFF )

# CloudCompare 'EDL' plugin
if (INSTALL_QEDL_PLUGIN)
    project( QEDL_PLUGIN )
    
    set( CC_SHADER_FOLDER EDL )
    include( ../CMakePluginTpl.cmake )
endif()
