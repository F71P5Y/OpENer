# Add sample application
add_subdirectory(sample_application)

# Platform-specific sources
set(PLATFORM_SPEC_SRC
    networkhandler.c
    opener_error.c
    networkconfig.c
)

# Optional: OpENer RT patch
set(OpENer_RT OFF CACHE BOOL "Activate OpENer RT")
if(OpENer_RT)
  set(OpENer_RT_Additional_Stacksize "10240" CACHE STRING "Additional stack size above the defined minimum")
  add_definitions(-DOPENER_RT)
  add_definitions(-DOPENER_RT_THREAD_SIZE=${OpENer_RT_Additional_Stacksize})
endif()

# Optional: AFL Fuzzing
if(USE_FUZZ_AFL)
  add_definitions(-DFUZZING_AFL)
endif()

# Zephyr library for this platform
zephyr_library()

zephyr_library_sources(
    ${PLATFORM_SPEC_SRC}
)

zephyr_include_directories(
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}/sample_application
)

# Link with other Zephyr libraries
zephyr_library_link_libraries(
    PLATFORM_GENERIC
    CIP
    Utils
    SAMPLE_APP
    ENET_ENCAP
    NVDATA
    rt
    c
    pthread
)

# Additional CIP objects
string(COMPARE NOTEQUAL "${OpENer_ADD_CIP_OBJECTS}" "" OpENer_HAS_ADDITIONAL_OBJECT)
if(OpENer_HAS_ADDITIONAL_OBJECT)
  message(STATUS "Additional activated objects: ${OpENer_ADD_CIP_OBJECTS}")
  string(REPLACE " " ";" OpENer_ADD_CIP_OBJECTS_LIST ${OpENer_ADD_CIP_OBJECTS})
  foreach(CIP_OBJECT IN LISTS OpENer_ADD_CIP_OBJECTS_LIST)
    zephyr_include_directories(${${CIP_OBJECT}_SOURCE_DIR})
    zephyr_library_link_libraries(${CIP_OBJECT})
  endforeach()
else()
  message(STATUS "No additional activated objects")
endif()
