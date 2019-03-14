#*******************************************************************************
#  Copyright (c) 2017 IBM Corp.
#
#  All rights reserved. This program and the accompanying materials
#  are made available under the terms of the Eclipse Public License v1.0
#  and Eclipse Distribution License v1.0 which accompany this distribution.
#
#  The Eclipse Public License is available at
#     http://www.eclipse.org/legal/epl-v10.html
#  and the Eclipse Distribution License is available at
#    http://www.eclipse.org/org/documents/edl-v10.php.
#
#  Contributors:
#     Ian Craggs - initial version
#*******************************************************************************/

# MQTTPacket Library
file(GLOB MQTTPacket_SOURCES "*.c")
file(GLOB MQTTPacket_INCLUDE_HEADERS "*.h")
add_library(paho-embed-mqtt3c SHARED ${MQTTPacket_SOURCES})
install(TARGETS paho-embed-mqtt3c DESTINATION ${CMAKE_INSTALL_PREFIX}/lib)
install(FILES ${MQTTPacket_INCLUDE_HEADERS} DESTINATION ${CMAKE_INSTALL_PREFIX}/include/paho)
target_compile_definitions(paho-embed-mqtt3c PRIVATE MQTT_SERVER MQTT_CLIENT)

add_library(MQTTPacketClient SHARED MQTTFormat MQTTPacket
            MQTTSerializePublish MQTTDeserializePublish
            MQTTConnectClient MQTTSubscribeClient MQTTUnsubscribeClient)
target_compile_definitions(MQTTPacketClient PRIVATE MQTT_CLIENT)

add_library(MQTTPacketServer SHARED MQTTFormat MQTTPacket
            MQTTSerializePublish MQTTDeserializePublish
            MQTTConnectServer MQTTSubscribeServer MQTTUnsubscribeServer)
target_compile_definitions(MQTTPacketServer PRIVATE MQTT_SERVER)
