cmake_minimum_required(VERSION 2.8.9)

project (bluetooth)

include_directories(/usr/include/glib-2.0)
include_directories(/usr/lib/x86_64-linux-gnu/glib-2.0/include)
include_directories(/usr/include/dbus-1.0)
include_directories(/usr/lib/x86_64-linux-gnu/dbus-1.0/include)
include_directories(vendors/bluez)

add_definitions(-DBLUETOOTH_PLUGIN_BUILTIN -DOBEX_PLUGIN_BUILTIN -D_FILE_OFFSET_BITS=64 -DHAVE_CONFIG_H)
set(VERSION "5.63")
set(CONFIGDIR "/usr/local/etc/bluetooth")
set(STORAGEDIR "/var/lib/bluetooth")
set(PLUGINDIR "/usr/local/lib/bluetooth/plugins")

file(GLOB SHARED_SOURCES    "vendors/bluez/src/shared/ad.c"
                            "vendors/bluez/src/shared/att.c"
                            "vendors/bluez/src/shared/btsnoop.c"
                            "vendors/bluez/src/shared/crypto.c"
                            "vendors/bluez/src/shared/ecc.c"
                            "vendors/bluez/src/shared/gap.c"
                            "vendors/bluez/src/shared/gatt-client.c"
                            "vendors/bluez/src/shared/gatt-db.c"
                            "vendors/bluez/src/shared/gatt-helpers.c"
                            "vendors/bluez/src/shared/gatt-server.c"
                            "vendors/bluez/src/shared/hci-crypto.c"
                            "vendors/bluez/src/shared/hci.c"
                            "vendors/bluez/src/shared/hfp.c"
                            "vendors/bluez/src/shared/io-glib.c"
                            "vendors/bluez/src/shared/log.c"
                            "vendors/bluez/src/shared/mainloop-glib.c"
                            "vendors/bluez/src/shared/mainloop-notify.c"
                            "vendors/bluez/src/shared/mgmt.c"
                            "vendors/bluez/src/shared/pcap.c"
                            "vendors/bluez/src/shared/queue.c"
                            "vendors/bluez/src/shared/ringbuf.c"
                            "vendors/bluez/src/shared/shell.c"
                            "vendors/bluez/src/shared/tester.c"
                            "vendors/bluez/src/shared/timeout-glib.c"
                            "vendors/bluez/src/shared/uhid.c"
                            "vendors/bluez/src/shared/util.c")

file(GLOB SRC_SOURCES   "vendors/bluez/src/adapter.c"
                        "vendors/bluez/src/adv_monitor.c"
                        "vendors/bluez/src/advertising.c"
                        "vendors/bluez/src/agent.c"
                        "vendors/bluez/src/backtrace.c"
                        "vendors/bluez/src/battery.c"
                        "vendors/bluez/src/dbus-common.c"
                        "vendors/bluez/src/device.c"
                        "vendors/bluez/src/eir.c"
                        "vendors/bluez/src/error.c"
                        "vendors/bluez/src/gatt-client.c"
                        "vendors/bluez/src/gatt-database.c"
                        "vendors/bluez/src/log.c"
                        "vendors/bluez/src/plugin.c"
                        "vendors/bluez/src/profile.c"
                        "vendors/bluez/src/rfkill.c"
                        "vendors/bluez/src/sdp-client.c"
                        "vendors/bluez/src/sdp-xml.c"
                        "vendors/bluez/src/sdpd-database.c"
                        "vendors/bluez/src/sdpd-request.c"
                        "vendors/bluez/src/sdpd-server.c"
                        "vendors/bluez/src/sdpd-service.c"
                        "vendors/bluez/src/service.c"
                        "vendors/bluez/src/storage.c"
                        "vendors/bluez/src/textfile.c"
                        "vendors/bluez/src/uuid-helper.c")

file(GLOB PLUGINS_SOURCES   "vendors/bluez/plugins/autopair.c"
                            "vendors/bluez/plugins/hostname.c"
                            "vendors/bluez/plugins/policy.c"
                            "vendors/bluez/plugins/wiimote.c")

file(GLOB PROFILES_SOURCES  "vendors/bluez/profiles/audio/a2dp.c"
                            "vendors/bluez/profiles/audio/avctp.c"
                            "vendors/bluez/profiles/audio/avdtp.c"
                            "vendors/bluez/profiles/audio/avrcp.c"
                            "vendors/bluez/profiles/audio/control.c"
                            "vendors/bluez/profiles/audio/media.c"
                            "vendors/bluez/profiles/audio/player.c"
                            "vendors/bluez/profiles/audio/sink.c"
                            "vendors/bluez/profiles/audio/source.c"
                            "vendors/bluez/profiles/audio/transport.c"
                            
                            "vendors/bluez/profiles/battery/bas.c"
                            "vendors/bluez/profiles/battery/battery.c"
                            
                            "vendors/bluez/profiles/deviceinfo/deviceinfo.c"
                            "vendors/bluez/profiles/deviceinfo/dis.c"
                            
                            "vendors/bluez/profiles/gap/gas.c"
                            
                            "vendors/bluez/profiles/input/device.c"
                            "vendors/bluez/profiles/input/hog-lib.c"
                            "vendors/bluez/profiles/input/hog.c"
                            "vendors/bluez/profiles/input/manager.c"
                            "vendors/bluez/profiles/input/server.c"
                            "vendors/bluez/profiles/input/suspend-none.c"
                            
                            "vendors/bluez/profiles/network/bnep.c"
                            "vendors/bluez/profiles/network/connection.c"
                            "vendors/bluez/profiles/network/manager.c"
                            "vendors/bluez/profiles/network/server.c"
                            
                            "vendors/bluez/profiles/scanparam/scan.c"
                            "vendors/bluez/profiles/scanparam/scpp.c"
                            
                            "vendors/bluez/profiles/heartrate/heartrate.c")

file(GLOB BTIO_SOURCES "vendors/bluez/btio/btio.c")

file(GLOB ATTRIB_SOURCES    "vendors/bluez/attrib/att.c"
                            "vendors/bluez/attrib/gatt.c"
                            "vendors/bluez/attrib/gattrib.c")

file(GLOB LIB_SOURCES   "vendors/bluez/lib/bluetooth.c"
                        "vendors/bluez/lib/hci.c"
                        "vendors/bluez/lib/sdp.c"
                        "vendors/bluez/lib/uuid.c")

file(GLOB GDBUS_SOURCES "vendors/bluez/gdbus/client.c"
                        "vendors/bluez/gdbus/mainloop.c"
                        "vendors/bluez/gdbus/object.c"
                        "vendors/bluez/gdbus/polkit.c"
                        "vendors/bluez/gdbus/watch.c")

file(GLOB SOURCES "vendors/bluez/src/main.c")

add_executable(bluetoothd   ${SOURCES} 
                            ${SHARED_SOURCES} 
                            ${SRC_SOURCES}
                            ${PLUGINS_SOURCES}
                            ${PROFILES_SOURCES}
                            ${BTIO_SOURCES}
                            ${ATTRIB_SOURCES}
                            ${LIB_SOURCES}
                            ${GDBUS_SOURCES})
target_link_libraries(bluetoothd glib-2.0 dbus-1 bluetooth readline dl)
target_compile_definitions(bluetoothd   PRIVATE "VERSION=\"${VERSION}\""
                                        PRIVATE "CONFIGDIR=\"${CONFIGDIR}\""
                                        PRIVATE "STORAGEDIR=\"${STORAGEDIR}\""
                                        PRIVATE "PLUGINDIR=\"${PLUGINDIR}\"")