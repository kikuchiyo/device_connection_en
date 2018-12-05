Sending device telemetry based on EnOS device protocol standard
============================================================

EnOS provides device SDKs for you to configure devices. These device SDKs already encapsulate protocols for data exchange between devices and EnOS Cloud. 

When the device SDKs provided by EnOS cannot meet your requirements, you can refer to this article to develop your own communication protocol based on the EnOS device protocol standard, which defines the data format of the MQTT-based transmission between devices and EnOS cloud. You can connect your devices into EnOS as long as your data format conforms to the standard.

The supported MQTT version:

- MQTT v3.1.1 on port 11883 if you use the secret-based one-way authentication.
- MQTT v3.1.1 over SSL/TLS on port 18883 if you use the certificate-based two-way authentication.


Common Parameter Description
=============================

The following table describes the common parameters used in the request and response messages.

.. list-table::
  :header-rows: 1

  * - Parameter
    - Type
    - Occurrence
    - Description
  * - id
    - String
    - Optional
    - Message ID. Reserved parameter for future   use.
  * - version
    - String
    - Mandatory
    - Version of the protocol.
  * - params
    - JSON
    - Mandatory in request
    - Request parameters, in JSON format, Can   either be arry or dict.
  * - method
    - String
    - Mandatory in request
    - Name of the method.
  * - code
    - Integer
    - Mandatory in response
    - Response code.
  * - data
    - JSON
    - Optional
    - Detailed infomaton, in JSON format. Can be   either int or dict regarded to the returned message.  





Connection Establishment
===================
Before develop any communication protocol, you should establish the communication with EnOS Cloud.

Please refer to the following section.

`Establishing communicate with EnOS Cloud using the MQTT protocol <nonsdk_login>`__

.. toctree::
  :maxdepth: 1
  :hidden:

  nonsdk_login



Protocol Standards
===================

From the data transmission direction perspective, the device protocol standards falls into two groups: upstream and downstream.

Please refer to the following sections.

.. toctree::
  :caption: Upstream
  :maxdepth: 1

  upstream/device_registration
  upstream/topological_mgmt/index
  upstream/device_connection/index
  upstream/device_tags/index
  upstream/device_else/index



.. toctree::
  :caption: Downstream
  :maxdepth: 1

  downstream/devices/index
  downstream/subdevices/index
