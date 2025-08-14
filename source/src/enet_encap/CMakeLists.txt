# Ethernet encapsulation library

set(ENET_ENCAP_SRC
    cpf.c
    encap.c
    endianconv.c
)

# Zephyr library definition
zephyr_library()

zephyr_library_sources(
    ${ENET_ENCAP_SRC}
)

zephyr_include_directories(
    ${CMAKE_CURRENT_SOURCE_DIR}
)

# Link with other Zephyr libraries
zephyr_library_link_libraries(Utils)
