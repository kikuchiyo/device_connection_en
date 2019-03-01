Device-End Development
=========================

EnOS™ provides device SDKs that encapsulates protocols for data transmission between devices and EnOS Cloud.

When the device SDKs provided by EnOS cannot meet your requirements, you can refer to this article to send telemetries into EnOS Cloud based on the EnOS device protocol standards, which defines the data format of the MQTT-based transmission between devices and EnOS cloud. You can connect your devices into EnOS as long as your data format conforms to the standard.

Prerequisites
--------------

Complete the cloud configuration in the EnOS Console and obtain the following information that are needed in the device-end ddevelopment:

- Device credentials for authentication
- Topics to subscribe data from and publish data to

.. toctree::
   :maxdepth: 1

   using_java_sdk
   using_non_sdk
