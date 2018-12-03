# Establishing communicate with EnOS Cloud using the MQTT protocol

This article instructs how to connect device through the MQTT to communication with EnOS Cloud.


The supported MQTT version:

- MQTT v3.1.1 on port 8883<!--小蔡确认-->
- MQTT v3.1.1 over WebSocket on port 443.<!--小蔡确认-->


All device communication with IoT Hub must be secured using TLS/SSL. Therefore, IoT Hub doesn’t support non-secure connections over port 1883.<!--小蔡确认-->



## Using the MQTT protocol directly

You can connect to the device end using the MQTT protocol on port 8883. In the CONNECT packet the device should use the following values:


```
  mqttClientId: clientId+"|securemode=2,signmethod=hmacsha1,timestamp=132323232|"

  mqttUsername: deviceKey+"&"+productKey
  mqttPassword: uppercase(sign_hmac(deviceSecret,content))
 ```


 - For the **mqttClientId** field:
   + _clientId_ can be specified using either MAC address or device serial number. It cannot be empty and must contain no more than 64 characters. The parameters within  ``||`` are the optional parameters.
   + _securemode_ is the secure mode that has been used. Currently, only support securemode=2.
   + _signmethod_ is the method of sign. Currently, only support signmethod=hmacsha1.
   + _timestamp_ is the current time in milliseconds.
 - For the **mqttUsername** field:
   + The value of the _deviceKey_ and _productKey_ can be found in the EnOS Console.
 - For the **mqttPassword** field:
   + The value of the _deviceSecret_ can be found in the EnOS Console.
   + _content_ is consistent of the _productKey_, _deviceKey_, _timestamp_, and _clientID_. The value must be sorted in alphabetical order and concatenated without concatenation symbols.  
    **NOTE** The value of the timestamp must be same as the timestamp in mqttClientID.




 Below is an example in python when clientId = 123, deviceKey = test, productKey = 123, timestamp = 1524448722000, deviceSecret=deviceSecret.<!--小蔡确认-->

```from paho.mqtt import client as mqtt
import ssl

path_to_root_cert = "<local path to digicert.cer>"
device_id = "<device id from device registry>"
sas_token = "<generated SAS token>"
iot_hub_name = "<iot hub name>"

def on_connect(client, userdata, flags, rc):
  print ("Device connected with result code: " + str(rc))
def on_disconnect(client, userdata, rc):
  print ("Device disconnected with result code: " + str(rc))
def on_publish(client, userdata, mid):
  print ("Device sent message")

client = mqtt.Client(client_id=device_id, protocol=mqtt.MQTTv311)

client.on_connect = on_connect
client.on_disconnect = on_disconnect
client.on_publish = on_publish

client.username_pw_set(username=iot_hub_name+".azure-devices.net/" + device_id, password=sas_token)

client.tls_set(ca_certs=path_to_root_cert, certfile=None, keyfile=None, cert_reqs=ssl.CERT_REQUIRED, tls_version=ssl.PROTOCOL_TLSv1, ciphers=None)
client.tls_insecure_set(False)

client.connect(iot_hub_name+".azure-devices.net", port=8883)

client.publish("devices/" + device_id + "/messages/events/", "{id=123}", qos=1)
client.loop_forever()
```
