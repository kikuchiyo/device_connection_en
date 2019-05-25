# Offline Message Integration

Users can use the offline message integration feature to import the historical data from a 3rd-party system into EnOS. Also, users can set policies to process, store and analyze the integrated data.

The offline message integration feature supports only one-way data transfer, i.e. from a 3rd-party system to EnOS. Use this feature in the following scenarios:

- Importing of the historical device data from a 3rd-party system.
- Breakpoint resume for cached device data. For example, the measure point data cached when a device is offline should be re-reported to the 3rd-party system and then transferred to EnOS once the device gets online. 

## Protocol Supported

EnOS can import historical data and offline cached data in a 3rd-party system by using the following protocols:

- MQTT. For details about the MQTT topics used for offline message integration, request and response formats, and parameter descriptions, see [MQTT Protocol-based Device Connectivity (Offline Message)](../../reference/mqtt_offline/index)

## Process

How the historical data and offline cached data of a 3rd-party system are integrated into EnOS by using MQTT is shown as follows:

.. image:: ../../media/offline_message_integration_mqtt.png

1. In EnOS, create a model and a product that uses the model.

2. Create a device that belongs to the product, whose data is to be integrated on EnOS in advance;

3. On EnOS, create an MQTT message channel and obtain the following parameters:
  - Broker URL
  - ClientID
  - Username
  - Password
  To obtain the parameters, on the EnOS console, select **Device Management > Message Integration**, then select **Details** on the created message channel. Then you can find these parameters in Details.

4. On the 3rd-party system, configure the parameters required to initialize the MQTT message channel, i.e. MQTT parameters stated in the previous step;

5. The 3rd-party system sends a request to set up connection.

6. The 3rd-party system is authenticated. EnOS subscribes to the topics for offline message integration.

7. EnOS sends a reponse indicating authentication success.

8. The 3rd-party system publishes the offline messages to specified MQTT topics. An independent broker is responsible for data publishing and subcription beteen the 3rd-party system and EnOS rather than reusing the existing broker that is used for real-time data publishing and subscription.

9. (Optional) If raw data of a device (e.g. binary data) is passed through by the 3rd-party system, EnOS would use the data parsing script to convert raw data into EnOS-defined JSON format.

10. EnOS detects the DeviceKey carried in the historical messaged reported by the 3rd-party system:
  - If the user have not registered the device on EnOS, EnOS would report an error in the log and the historical data cannot be integrated. <!--The descriptions here should be modified if automatic device registration is supporter later. -->
  - If the deviceKey exists, the historical data would be saved;

11. EnOS sends a response to the 3rd-party system indicating integration success.

12. The user can view the historical message integrated on EnOS.

.. note:: 1. To view the message log for the channel, select **Device Management > Message Integration**. Then select the message channel and click **Details**. Then you can see the log. The message log includes the following information:
  - Channel connection information such as MQTT connection/disconnection records;
  - Payload transmission log;
  - Error log such as JSON format verification failure or script invocation error.

For more information about creating offline message channels, see [Creating Offline Message Channel](../../howto/device/manage/creating_offline_message_integration_channel).

## Offline Message Usage

After the historical messages of the 3rd-party system are integrated into EnOS, applications can call use the data by calling EnOS APIs. For more information, see API documents. 

In addition, the user can subscribe to offline message data streams on EnOS, and the offline data are published to the corresponding Kafka topics through the rule engine and then be available for subscription by data asset management functions.


