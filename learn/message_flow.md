# MQTT-Based Connection

As shown in the figure below, a device can be connected directly or through the edge to the EnOS IoT Hub via MQTT protocol. MQTT is a lightweight open-source IoT protocol based on TCP/IP. EnOS's MQTT protocol supports the following features:

  - Topic-based subscription and publish of data, communication resources are segregated by topic to prevent devices from accessing unauthorized data.

  - RRPC

.. image:: ../media/device_connection_methods.png

Data is sent to the EnOS Cloud via the IoT Hub and distributed by the rule engine to different storage or functional modules for further processing.

<!--
- Redis database: for real-time access of hot data
- Time series database
- Alert engine: for real-time monitoring of device alerts
- Stream processing engine: for stream processing such as to clease the real-time data, to calculate results based on business needs such as to calculate the average data for a batch of devices.
-->

The following functional modules and concepts are involved in the message flow:

## IoT Hub

IoT Hub is a cloud broker service that EnOS provides for device connection.

The cloud broker provides the following functions:

- Safe and reliable large-scale bi-directional message transmission from the devices to the cloud.
- Exposing interface for connections from MQTT clients.
- Forwarding the data from the client to corresponding subscribers, i.e. services and applications on EnOS™.
- Providing license authorization and creation of thing and policy themes.


## EnOS Edge

Edge is the front end of Envision EnOS IoT platform for data acquisition. It is used to collect on-site device data or connected to a third party system for data acquisition and transmission of data to the EnOS Cloud.

Edge, as software, supports data acquisition, multiple communication conventions, local caching and breakpoint continuation. It can either be deployed in a cloud machine or an on-site hardware of a specified brand model. An edge must have a legal serial number (SN) assigned by Envision to be recognized by EnOS Cloud. For more information, see [EnOS Edge Overview](https://www.envisioniot.com/docs/enos-edge/en/latest/edge_overview.html)

## Connection Scenarios

Based on whether and where the edge device is used in the connection. The following connection scenarios are supported:

### Scenario 1: Connect directly to EnOS IoT Hub

This method requires the devices to support MQTT protocol and is applicable to most of the smart IoT devices.

### Scenario 2: Connect through remote EnOS Edge

In this case, the EnOS Edge is deployed remotely at the cloud side. This method mainly applies to traditional devices and systems that do not support the MQTT protocol.

### Scenario 3: Connect through on-site EnOS Edge

In this case, the EnOS Edge is deployed on-site with the devices. This method mainly applies to traditional devices and systems that do not support the MQTT protocol. Compared with scenario 2, this connection method can facilitate breakpoint resumption in the case of network interruption between the Edge and cloud. When a network interuption occurs, the Edge can cache data automatically during the interruption and resume data upload starting from the breakpoint when the connection recovers.

### Scenario 4: Connect through EnOS™ Cloud Edge clusters (cloud service)

This requires that the device to be connected has a unique ID and can upload data through supported communication protocols. This method is frequently used for the photovoltaic device connection.
