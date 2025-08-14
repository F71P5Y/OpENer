# CIP library

zephyr_library()

zephyr_library_sources(
    appcontype.c
    cipassembly.c
    cipclass3connection.c
    cipcommon.c
    cipconnectionobject.c
    cipconnectionmanager.c
    cipdlr.c
    cipethernetlink.c
    cipidentity.c
    cipioconnection.c
    cipmessagerouter.c
    ciptcpipinterface.c
    ciptypes.c
    cipepath.c
    cipelectronickey.c
    cipstring.c
    cipstringi.c
    cipqos.c
)

zephyr_include_directories(${CMAKE_CURRENT_SOURCE_DIR})

zephyr_library_link_libraries(ENET_ENCAP)
