
set(TARGET_NAME pantheon-photos-publishing-extra)
vala_precompile (VALA_C ${TARGET_NAME}
    shotwell-publishing-extras.vala
    YandexPublishing.vala
    TumblrPublishing.vala
    Resources.vala
    RESTSupport.vala
CUSTOM_VAPIS
    ${CMAKE_SOURCE_DIR}/vapi/config.vapi
    ${CMAKE_BINARY_DIR}/src/${CMAKE_PROJECT_NAME}.vapi
PACKAGES
    ${DEPS_PACKAGES}
OPTIONS
    ${GLOBAL_VALA_OPTIONS}
)

add_library(${TARGET_NAME} MODULE ${VALA_C})

include_directories (${CMAKE_SOURCE_DIR}/vapi)
target_link_libraries(${TARGET_NAME} ${DEPS_LIBRARIES})
add_dependencies(${TARGET_NAME} ${EXEC_NAME})

install(TARGETS ${TARGET_NAME} DESTINATION ${BUILTIN_DIR})

# Install custom icons
file (GLOB ICON_FILES *.png)
install (FILES ${ICON_FILES} DESTINATION ${BUILTIN_DIR})

# Install UI files
file (GLOB UI_FILES *.glade)
install (FILES ${UI_FILES} DESTINATION ${BUILTIN_DIR})
