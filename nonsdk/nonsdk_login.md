# Establishing Connection with EnOS Cloud using the MQTT Protocol

This article instructs how to establish connection from devices to the EnOS Cloud through the MQTT protocol.


The supported MQTT version:

- MQTT v3.1.1 on port 11883 if you use the secret-based one-way authentication.
- MQTT v3.1.1 over SSL/TLS on port 18883 if you use the certificate-based two-way authentication.


## Using the MQTT Protocol Directly

You can connect devices to the EnOS Cloud using the MQTT protocol directly. Include the following values in the CONNECT packet of the device:

```
  mqttClientId: clientId+"|securemode=2,signmethod=hmacsha1,timestamp=132323232|"

  mqttUsername: deviceKey+"&"+productKey
  mqttPassword: uppercase(sign_hmac(deviceSecret,content))
 ```


 - For the **mqttClientId** segment:
   - _clientId_: Mandatory. Can be specified using either the MAC address or device serial number. It must contain no more than 64 characters. The parameters within  ``||`` are the optional parameters.
   - _securemode_: Optional. Indicates the secure mode that has been used. Currently, only support securemode=2.
   - _signmethod_: Optional. Indicates the signing method. Currently, only support `signmethod=hmacsha1`.
   - _timestamp_: Optional. Indicates the current time in milliseconds.

 - For the **mqttUsername** segment:
   - The value of the _deviceKey_ and _productKey_ of a device can be obtained from the EnOS Console after you complete provisioning the device.

 - For the **mqttPassword** segment:
   - The value of the _deviceSecret_ can be obtained from the EnOS Console.
   - _content_ is the concatenation of _productKey_, _deviceKey_, _timestamp_, and _clientID_. The values must be sorted in alphabetical order and concatenated without concatenation symbols.  
     Below is an example of _content_ when clientId=123, deviceKey=test, productKey=123, timestamp=1524448722000, deviceSecret=deviceSecret.
     ```
     sign= toUpperCase(hmacsha1(clientId123deviceKeytestproductKey123timestamp1524448722000deviceSecret))
     ```

     **NOTE**: The value of `timestamp` must be same as the `timestamp` in the **mqttClientId** segment.
