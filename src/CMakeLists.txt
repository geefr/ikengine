
# libikengine
include( sources )

configure_file( ${CMAKE_CURRENT_SOURCE_DIR}/config.h.in 
                ${CMAKE_CURRENT_BINARY_DIR}/config.h )

if( ENABLE_DYNAMIXEL )
  list( APPEND LIBIKENGINE_SRCS ${LIBIKENGINE_LIBDXL_SRCS} )
  list( APPEND LIBIKENGINE_LINK dynamixel_sdk )
endif()
include_directories( 
  ${CMAKE_CURRENT_SOURCE_DIR}
  ${DYNAMIXELSDK_INCLUDE_DIR}
  ${EIGEN3_INCLUDE_DIR} )

if( IKENGINE_OSG )
  list( APPEND LIBIKENGINE_LINK osg )
endif()

add_library( ikengine SHARED ${LIBIKENGINE_SRCS} )
target_link_libraries( ikengine ${LIBIKENGINE_LINK} )

install( TARGETS ikengine
         RUNTIME DESTINATION bin
         LIBRARY DESTINATION lib
         ARCHIVE DESTINATION lib )
install( DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/
         DESTINATION include 
         FILES_MATCHING PATTERN *.h )
install( DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/
         DESTINATION include
         FILES_MATCHING PATTERN config.h )

