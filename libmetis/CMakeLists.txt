# Add this directory for internal users.
include_directories(.)

# Find sources.
file(GLOB metis_sources *.c)

# Build libmetis.
add_library(metis ${METIS_LIBRARY_TYPE} ${metis_sources})
target_include_directories(metis
    PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}/../include
)
target_link_libraries(metis
    PRIVATE
    GKlib
)
target_compile_definitions(metis PUBLIC
    IDXTYPEWIDTH=${METIS_IDX_BITS}
    REALTYPEWIDTH=${METIS_REAL_BITS}
)

if(METIS_INSTALL)
    install(TARGETS metis
        LIBRARY DESTINATION lib
        RUNTIME DESTINATION lib
        ARCHIVE DESTINATION lib)
endif()
