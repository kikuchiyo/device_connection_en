# Device Provisioning

The EnOS™ Device Provisioning function helps IoT engineers to manage the device lifecycle, establish connection from the devices to the EnOS Cloud, and secure the two-way communication between the devices and the cloud.

## Major Functionalities

The EnOS Device Provisioning function provides the following key functionalities:

### Device Connection

Provides device SDK to allow devices to connect to the IoT Hub.
- Provides MQTT device SDK to meet the real-time requirements for long connections and low power requirements for short connections.
- Provides connection schemes such as direct device connection and indirect connection through gateway proxies, providing solutions to meet the requirements of various scenarios for the heterogeneous network devices of enterprises.

### Device Management

Supports complete device lifecycle management, including:
- Device registration
- Device configuration
- Remote control
- Firmware upgrade
- Real-time monitoring
- Device logout

### Model Management

Provides device models. The device model allows devices of thousands of models from different manufacturers to be unified into a small number of common models and thus simplifies application development.

### Device and Cloud Security

**Authentication**

- Supports _secret-per-device_ authentication mechanism, reducing the security risk that the device may be hacked. This machanism is suitable for devices that can be burned with pre-allocated device key into each chip in batches. Each device carries a unique key-secret pair as the device leaves the factory.

- Supports _secret-per-product_ mechanism, where devices of the same product model are pre-burned with key-secret pair (the _product key-secret pair_). The device can dynamically acquire the device secret during authentication. This machanism is suitable for situations where unique key-secret pairs cannot be burned into each device in mass production.

For more information, see [Device Authentication Mechanism](deviceconnection_authentication).

**Communication and Data Security**

- Encrypts and decrypts data through the CA certificate mechanism to ensure the security of communication between the device and the cloud.

- Segregates communication resources by topic to prevent devices from accessing unauthorized data.


## Message Flow and Relevant Concepts

As shown in the figure below, a device can be connected directly or through the edge to the EnOS IoT Hub. The EnOS IoT Hub accepts direct-connecting devices or edges to communicate via the MQTT protocol. MQTT is a lightweight open-source IoT protocol based on TCP/IP. EnOS's MQTT protocol supports the following features:

- Topic-based subscription and publish of data
- RRPC

.. image:: media/device_connection_methods.png
   :width: 700px

Data is sent to the EnOS Cloud via the IoT Hub and distributed by the rule engine to different storage or functional modules for further processing:

- Time series database
- Alert engine
- Stream computing engine

The following functional modules and concepts are involved in the message flow:

### IoT Hub

IoT Hub is a cloud broker service that EnOS provides for device connection.

The cloud broker provides the following functions:

- Safe and reliable large-scale bi-directional message transmission from the devices to the cloud.
- Forwarding the data from the client to corresponding subscribers on EnOS™.
- Providing license authorization and creation of thing and policy themes.
- Exposing interface for connections from MQTT clients.

### EnOS Edge

Edge is the front end of Envision EnOS IoT platform for data acquisition. It is used to collect on-site device data or connected to a third party system for data acquisition and transmission of data to the EnOS Cloud.

Edge, as software, supports data acquisition, multiple communication conventions, local caching and breakpoint continuation. It can either be deployed in a cloud machine or an on-site hardware of a specified brand model. An edge must have a legal serial number (SN) assigned by Envision to be recognized by EnOS Cloud. For more information, see [EnOS Edge Overview](https://www.envisioniot.com/docs/enos-edge/en/latest/edge_overview.html)

### Topic

A topic is the theme of messages. A topic takes one connection channel, which a device can subscribe and publish messages to. When you provision a device, you must configure the topic name for the device. When the device successfully establishes connection to the EnOS Cloud, the device can publish or subscribe to this topic.

## Connection Scenarios

Based on whether and where the edge device is used in the connection. The following connection scenarios are supported:

**Scenario 1: Connect through EnOS IoT Hub via MQTT protocol (cloud service)**

This method requires the devices to support MQTT protocol and is applicable to most of the new IoT devices.

**Scenario 2: Connect through on-site EnOS Edge**

In this case, the EnOS Edge is deployed on-site with the devices. This method mainly applies to traditional devices and systems that do not support the MQTT protocol.

**Scenario 3: Connect through remote EnOS Edge**

In this case, the EnOS Edge is deployed remotely at the cloud side. This method mainly applies to traditional devices and systems that do not support the MQTT protocol.

**Scenario 4: Connect through EnOS™ Cloud Edge clusters (cloud service)**

This requires that the device to be connected has a unique ID and can upload data through supported communication protocols. This method is frequently used for the photovoltaic device connection.

## Related Information

- [Getting Started With Direct Device Connection](gettingstarted_device_connection)
- [Getting Started With Connecting Sub-device to EnOS Cloud via Edge](gettingstarted_edge_connection)
