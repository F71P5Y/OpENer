# Utils library

zephyr_library()

zephyr_library_sources(
    random.c
    xorshiftrandom.c
    doublylinkedlist.c
    enipmessage.c
)

zephyr_include_directories(${CMAKE_CURRENT_SOURCE_DIR})
