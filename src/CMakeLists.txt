
########################################### BEGIN: GRAB SOURCE FILES ##########################################
FILE(GLOB ossim_SRCS  RELATIVE_PATH ${CMAKE_CURRENT_SOURCE_DIR} 
        "${CMAKE_CURRENT_SOURCE_DIR}/ossimConfig*.cpp" 
        "${CMAKE_CURRENT_SOURCE_DIR}/ossimVer*.cpp" 
        "${CMAKE_CURRENT_SOURCE_DIR}/init/*.cpp" "${CMAKE_CURRENT_SOURCE_DIR}/init/*.c" 
        "${CMAKE_CURRENT_SOURCE_DIR}/reg/*.cpp" "${CMAKE_CURRENT_SOURCE_DIR}/reg/*.c" 
        "${CMAKE_CURRENT_SOURCE_DIR}/base/*.cpp" "${CMAKE_CURRENT_SOURCE_DIR}/base/*.c" 
        "${CMAKE_CURRENT_SOURCE_DIR}/elevation/*.cpp" "${CMAKE_CURRENT_SOURCE_DIR}/elevation/*.c" 
        "${CMAKE_CURRENT_SOURCE_DIR}/font/*.cpp" "${CMAKE_CURRENT_SOURCE_DIR}/font/*.c" 
        "${CMAKE_CURRENT_SOURCE_DIR}/imaging/*.cpp" "${CMAKE_CURRENT_SOURCE_DIR}/imaging/*.c" 
        "${CMAKE_CURRENT_SOURCE_DIR}/matrix/*.cpp" "${CMAKE_CURRENT_SOURCE_DIR}/matrix/*.c" 
        "${CMAKE_CURRENT_SOURCE_DIR}/parallel/*.cpp" "${CMAKE_CURRENT_SOURCE_DIR}/parallel/*.c"
        "${CMAKE_CURRENT_SOURCE_DIR}/point_cloud/*.cpp" "${CMAKE_CURRENT_SOURCE_DIR}/point_cloud/*.c"
        "${CMAKE_CURRENT_SOURCE_DIR}/projection/*.cpp" "${CMAKE_CURRENT_SOURCE_DIR}/projection/*.c" 
        "${CMAKE_CURRENT_SOURCE_DIR}/support_data/*.cpp" "${CMAKE_CURRENT_SOURCE_DIR}/support_data/*.c" 
        "${CMAKE_CURRENT_SOURCE_DIR}/reg/*.cpp" "${CMAKE_CURRENT_SOURCE_DIR}/reg/*.c" 
        "${CMAKE_CURRENT_SOURCE_DIR}/util/*.cpp" "${CMAKE_CURRENT_SOURCE_DIR}/util/*.c" 
        "${CMAKE_CURRENT_SOURCE_DIR}/vec/*.cpp" "${CMAKE_CURRENT_SOURCE_DIR}/vec/*.c" 
        "${CMAKE_CURRENT_SOURCE_DIR}/video/*.cpp" "${CMAKE_CURRENT_SOURCE_DIR}/video/*.c"
        "${CMAKE_CURRENT_SOURCE_DIR}/vpfutil/*.cpp" "${CMAKE_CURRENT_SOURCE_DIR}/vpfutil/*.c"
        "${CMAKE_CURRENT_SOURCE_DIR}/plugin/*.cpp" "${CMAKE_CURRENT_SOURCE_DIR}/plugin/*.c")

IF(UNIX)
   FILE(GLOB ossim_sockets_SRCS RELATIVE_PATH ${CMAKE_CURRENT_SOURCE_DIR} "${CMAKE_CURRENT_SOURCE_DIR}/sockets/*.cpp")
   LIST(APPEND ossim_SRCS "${ossim_sockets_SRCS}")
ELSEIF(WIN32)
   FILE(GLOB ossim_dll_main_SRCS RELATIVE_PATH ${CMAKE_CURRENT_SOURCE_DIR} "${CMAKE_CURRENT_SOURCE_DIR}/dll_main/*.cpp")
  LIST(APPEND ossim_SRCS "${ossim_dll_main_SRCS}")
ENDIF(UNIX)
   
IF (OSSIM_HAS_HDF5)
   message( STATUS "HDF5 components will be included." )
   FILE(GLOB ossim_hdf5_SRCS RELATIVE_PATH ${CMAKE_CURRENT_SOURCE_DIR} "${CMAKE_CURRENT_SOURCE_DIR}/hdf5/*.cpp")
   LIST(APPEND ossim_SRCS "${ossim_hdf5_SRCS}")
ELSE (OSSIM_HAS_HDF5)
   message( STATUS "HDF5 components are being excluded from the build." )
ENDIF (OSSIM_HAS_HDF5)

IF (WIN32)
   IF (BUILD_SHARED)
      ADD_DEFINITIONS("-DOSSIMMAKINGDLL")
    ELSE (BUILD_SHARED)
      ADD_DEFINITIONS("-DOSSIM_STATIC")
   ENDIF (BUILD_SHARED)
ENDIF (WIN32)

############################### GRAB HEADERS #####################################
FILE(GLOB ossim_HDRS RELATIVE "${CMAKE_CURRENT_SOURCE_DIR}" "${CMAKE_CURRENT_SOURCE_DIR}/../include/ossim/*.h")
FILE(GLOB ossim_base_HDRS RELATIVE "${CMAKE_CURRENT_SOURCE_DIR}" "${CMAKE_CURRENT_SOURCE_DIR}/../include/ossim/base/*.h")
FILE(GLOB ossim_elevation_HDRS RELATIVE "${CMAKE_CURRENT_SOURCE_DIR}" "${CMAKE_CURRENT_SOURCE_DIR}/../include/ossim/elevation/*.h")
FILE(GLOB ossim_font_HDRS RELATIVE "${CMAKE_CURRENT_SOURCE_DIR}" "${CMAKE_CURRENT_SOURCE_DIR}/../include/ossim/font/*.h")
FILE(GLOB ossim_imaging_HDRS RELATIVE "${CMAKE_CURRENT_SOURCE_DIR}" "${CMAKE_CURRENT_SOURCE_DIR}/../include/ossim/imaging/*.h")
FILE(GLOB ossim_init_HDRS RELATIVE "${CMAKE_CURRENT_SOURCE_DIR}" "${CMAKE_CURRENT_SOURCE_DIR}/../include/ossim/init/*.h")
FILE(GLOB ossim_reg_HDRS RELATIVE "${CMAKE_CURRENT_SOURCE_DIR}" "${CMAKE_CURRENT_SOURCE_DIR}/../include/ossim/reg/*.h")
FILE(GLOB ossim_matrix_HDRS RELATIVE "${CMAKE_CURRENT_SOURCE_DIR}" "${CMAKE_CURRENT_SOURCE_DIR}/../include/ossim/matrix/*.h")
FILE(GLOB ossim_parallel_HDRS RELATIVE "${CMAKE_CURRENT_SOURCE_DIR}" "${CMAKE_CURRENT_SOURCE_DIR}/../include/ossim/parallel/*.h")
FILE(GLOB ossim_plugin_HDRS RELATIVE "${CMAKE_CURRENT_SOURCE_DIR}" "${CMAKE_CURRENT_SOURCE_DIR}/../include/ossim/plugin/*.h")
FILE(GLOB ossim_point_cloud_HDRS RELATIVE "${CMAKE_CURRENT_SOURCE_DIR}" "${CMAKE_CURRENT_SOURCE_DIR}/../include/ossim/point_cloud/*.h")
FILE(GLOB ossim_projection_HDRS RELATIVE "${CMAKE_CURRENT_SOURCE_DIR}" "${CMAKE_CURRENT_SOURCE_DIR}/../include/ossim/projection/*.h")
FILE(GLOB ossim_support_data_HDRS RELATIVE "${CMAKE_CURRENT_SOURCE_DIR}" "${CMAKE_CURRENT_SOURCE_DIR}/../include/ossim/support_data/*.h")
FILE(GLOB ossim_util_HDRS RELATIVE "${CMAKE_CURRENT_SOURCE_DIR}" "${CMAKE_CURRENT_SOURCE_DIR}/../include/ossim/util/*.h")
FILE(GLOB ossim_vec_HDRS RELATIVE "${CMAKE_CURRENT_SOURCE_DIR}" "${CMAKE_CURRENT_SOURCE_DIR}/../include/ossim/vec/*.h")
FILE(GLOB ossim_video_HDRS RELATIVE "${CMAKE_CURRENT_SOURCE_DIR}" "${CMAKE_CURRENT_SOURCE_DIR}/../include/ossim/video/*.h")
FILE(GLOB ossim_vpfutil_HDRS RELATIVE "${CMAKE_CURRENT_SOURCE_DIR}" "${CMAKE_CURRENT_SOURCE_DIR}/../include/ossim/vpfutil/*.h")

IF(UNIX)
  FILE(GLOB ossim_sockets_HDRS RELATIVE "${CMAKE_CURRENT_SOURCE_DIR}" "${CMAKE_CURRENT_SOURCE_DIR}/../include/ossim/sockets/*.h")
ENDIF(UNIX)

IF (OSSIM_HAS_HDF5)
  FILE(GLOB ossim_hdf5_HDRS RELATIVE "${CMAKE_CURRENT_SOURCE_DIR}" "${CMAKE_CURRENT_SOURCE_DIR}/../include/ossim/hdf5/*.h")
ENDIF (OSSIM_HAS_HDF5)

MESSAGE( "${ossim_HDRS}" )

IF(USE_OSSIM_JSONCPP)
   FILE(GLOB ossim_jsoncpp_HDRS RELATIVE "${CMAKE_CURRENT_SOURCE_DIR}" "${CMAKE_CURRENT_SOURCE_DIR}/../include/ossim/json/*.h")
   LIST(APPEND ossim_SRCS "${CMAKE_CURRENT_SOURCE_DIR}/json/jsoncpp.cpp")
ENDIF(USE_OSSIM_JSONCPP)

SET(OSSIM_HEADER_FILES
  ${ossim_HDRS} ${ossim_jsoncpp_HDRS}
  ${ossim_base_HDRS} ${ossim_elevation_HDRS} ${ossim_font_HDRS}  ${ossim_imaging_HDRS} 
  ${ossim_init_HDRS} ${ossim_reg_HDRS} ${ossim_matrix_HDRS} ${ossim_parallel_HDRS} ${ossim_plugin_HDRS} 
  ${ossim_point_cloud_HDRS} ${ossim_projection_HDRS} ${ossim_support_data_HDRS} ${ossim_util_HDRS} 
  ${ossim_vec_HDRS} ${ossim_video_HDRS} ${ossim_vpfutil_HDRS} ${ossim_sockets_HDRS} ${ossim_hdf5_HDRS} )


################################## APPLE Framework support deep header mapping ###################################
IF(APPLE)
  FOREACH(f  ${ossim_HDRS} )
      SET_SOURCE_FILES_PROPERTIES( ${f} PROPERTIES MACOSX_PACKAGE_LOCATION Headers )
  ENDFOREACH(f)
  FOREACH(f  ${ossim_base_HDRS} )
      SET_SOURCE_FILES_PROPERTIES( ${f} PROPERTIES MACOSX_PACKAGE_LOCATION Headers/base )
  ENDFOREACH(f)
  FOREACH(f  ${ossim_elevation_HDRS} )
      SET_SOURCE_FILES_PROPERTIES( ${f} PROPERTIES MACOSX_PACKAGE_LOCATION Headers/elevation )
  ENDFOREACH(f)
  FOREACH(f  ${ossim_font_HDRS} )
      SET_SOURCE_FILES_PROPERTIES( ${f} PROPERTIES MACOSX_PACKAGE_LOCATION Headers/font )
  ENDFOREACH(f)
  FOREACH(f  ${ossim_imaging_HDRS} )
      SET_SOURCE_FILES_PROPERTIES( ${f} PROPERTIES MACOSX_PACKAGE_LOCATION Headers/imaging )
  ENDFOREACH(f)
  FOREACH(f  ${ossim_init_HDRS} )
      SET_SOURCE_FILES_PROPERTIES( ${f} PROPERTIES MACOSX_PACKAGE_LOCATION Headers/init )
  ENDFOREACH(f)
  FOREACH(f  ${ossim_reg_HDRS} )
      SET_SOURCE_FILES_PROPERTIES( ${f} PROPERTIES MACOSX_PACKAGE_LOCATION Headers/reg )
  ENDFOREACH(f)
  FOREACH(f  ${ossim_matrix_HDRS} )
      SET_SOURCE_FILES_PROPERTIES( ${f} PROPERTIES MACOSX_PACKAGE_LOCATION Headers/matrix )
  ENDFOREACH(f)
  FOREACH(f  ${ossim_parallel_HDRS} )
      SET_SOURCE_FILES_PROPERTIES( ${f} PROPERTIES MACOSX_PACKAGE_LOCATION Headers/parallel )
  ENDFOREACH(f)
  FOREACH(f  ${ossim_plugin_HDRS} )
      SET_SOURCE_FILES_PROPERTIES( ${f} PROPERTIES MACOSX_PACKAGE_LOCATION Headers/plugin )
  ENDFOREACH(f)
  FOREACH(f  ${ossim_point_cloud_HDRS} )
      SET_SOURCE_FILES_PROPERTIES( ${f} PROPERTIES MACOSX_PACKAGE_LOCATION Headers/point_cloud )
  ENDFOREACH(f)
  FOREACH(f  ${ossim_projection_HDRS} )
      SET_SOURCE_FILES_PROPERTIES( ${f} PROPERTIES MACOSX_PACKAGE_LOCATION Headers/projection )
  ENDFOREACH(f)
  FOREACH(f  ${ossim_support_data_HDRS} )
      SET_SOURCE_FILES_PROPERTIES( ${f} PROPERTIES MACOSX_PACKAGE_LOCATION Headers/support_data )
  ENDFOREACH(f)
  FOREACH(f  ${ossim_util_HDRS} )
      SET_SOURCE_FILES_PROPERTIES( ${f} PROPERTIES MACOSX_PACKAGE_LOCATION Headers/util )
  ENDFOREACH(f)
  FOREACH(f  ${ossim_vec_HDRS} )
      SET_SOURCE_FILES_PROPERTIES( ${f} PROPERTIES MACOSX_PACKAGE_LOCATION Headers/vec )
  ENDFOREACH(f)
  FOREACH(f  ${ossim_video_HDRS} )
      SET_SOURCE_FILES_PROPERTIES( ${f} PROPERTIES MACOSX_PACKAGE_LOCATION Headers/video )
  ENDFOREACH(f)

  FOREACH(f  ${ossim_vpfutil_HDRS} )
     SET_SOURCE_FILES_PROPERTIES( ${f} PROPERTIES MACOSX_PACKAGE_LOCATION Headers/vpfutil )
  ENDFOREACH(f)

  IF (OSSIM_HAS_HDF5)
    FOREACH(f  ${ossim_hdf5_HDRS} )
      SET_SOURCE_FILES_PROPERTIES( ${f} PROPERTIES MACOSX_PACKAGE_LOCATION Headers/hdf5 )
    ENDFOREACH(f)
  ENDIF (OSSIM_HAS_HDF5)

  IF(USE_OSSIM_JSONCPP)
     SET_SOURCE_FILES_PROPERTIES( json.h PROPERTIES MACOSX_PACKAGE_LOCATION Headers/json )
  ENDIF(USE_OSSIM_JSONCPP)

ENDIF(APPLE)

#################################### SETUP the required link parameters using the Ossim macro ####################################
OSSIM_LINK_LIBRARY(${LIB_NAME} 
                   COMPONENT_NAME ossim 
                   TYPE ${OSSIM_USER_DEFINED_DYNAMIC_OR_STATIC}
                   LIBRARIES ${ossimDependentLibs}
                   HEADERS "${OSSIM_HEADER_FILES}" 
                   PUBLIC_HEADERS "${ossim_HDRS}"
                   SOURCE_FILES "${ossim_SRCS}"
                   INSTALL_LIB VERSION_SYMLINKS)

# The install headers was duplicating ossimVersion.h and ossimConfig.h in "install_prefix/include".
# INSTALL_HEADERS)

########################################################## If DO special case for ossim core needs to have the files mapped properly ################################ 
IF(NOT OSSIM_BUILD_FRAMEWORKS OR NOT APPLE)
   install(FILES ${ossim_HDRS} DESTINATION include/ossim COMPONENT ossim) 
   install(FILES ${ossim_base_HDRS} DESTINATION include/ossim/base COMPONENT ossim) 
   install(FILES ${ossim_elevation_HDRS} DESTINATION include/ossim/elevation COMPONENT ossim)
   install(FILES ${ossim_font_HDRS} DESTINATION include/ossim/font COMPONENT ossim)
   install(FILES ${ossim_imaging_HDRS} DESTINATION include/ossim/imaging COMPONENT ossim) 
   install(FILES ${ossim_init_HDRS} DESTINATION include/ossim/init COMPONENT ossim) 
   install(FILES ${ossim_reg_HDRS} DESTINATION include/ossim/reg COMPONENT ossim) 
   install(FILES ${ossim_matrix_HDRS} DESTINATION include/ossim/matrix COMPONENT ossim) 
   install(FILES ${ossim_parallel_HDRS} DESTINATION include/ossim/parallel COMPONENT ossim) 
   install(FILES ${ossim_plugin_HDRS} DESTINATION include/ossim/plugin COMPONENT ossim) 
   install(FILES ${ossim_point_cloud_HDRS} DESTINATION include/ossim/point_cloud COMPONENT ossim) 
   install(FILES ${ossim_projection_HDRS} DESTINATION include/ossim/projection COMPONENT ossim) 
   install(FILES ${ossim_support_data_HDRS} DESTINATION include/ossim/support_data COMPONENT ossim) 
   install(FILES ${ossim_util_HDRS} DESTINATION include/ossim/util COMPONENT ossim) 
   install(FILES ${ossim_vec_HDRS} DESTINATION include/ossim/vec COMPONENT ossim) 
   install(FILES ${ossim_video_HDRS} DESTINATION include/ossim/video COMPONENT ossim) 
   install(FILES ${ossim_vpfutil_HDRS} DESTINATION include/ossim/vpfutil COMPONENT ossim)
   IF(USE_OSSIM_JSONCPP)
      install(FILES ${ossim_jsoncpp_HDRS} DESTINATION include/ossim/json COMPONENT ossim)
   ENDIF(USE_OSSIM_JSONCPP)
   IF(UNIX)
     install(FILES ${ossim_sockets_HDRS} DESTINATION include/ossim/sockets COMPONENT ossim) 
   ENDIF(UNIX)
   IF (OSSIM_HAS_HDF5)
     install(FILES ${ossim_hdf5_HDRS} DESTINATION include/ossim/hdf5 COMPONENT ossim) 
  ENDIF (OSSIM_HAS_HDF5)
ENDIF(NOT OSSIM_BUILD_FRAMEWORKS OR NOT APPLE)
# ENDIF(NOT OSSIM_FRAMEWORK_GENERATION OR NOT APPLE)

# ---
# This is the old list of library for the link line.  Replaced with ${ossimDependentLibs}.  
# Kept temporarily in case I broke something.  drb - 31 Aug. 2011
# LIBRARIES ${JPEG_LIBRARIES} ${TIFF_LIBRARIES} ${GEOTIFF_LIBRARIES} ${OPENTHREADS_LIBRARIES} ${FREETYPE_LIBRARIES} ${MPI_LIBRARIES} ${ZLIB_LIBRARIES} ${DL_LIBRARY}
# ---
