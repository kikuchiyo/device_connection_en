# Establishing Communicate with EnOS Cloud using the MQTT Protocol

This article instructs how device connect to EnOS Cloud through the MQTT protocol.


The supported MQTT version:

- MQTT v3.1.1 on port 11883 if you use the secret-based one-way authentication.
- MQTT v3.1.1 over SSL/TLS on port 18883 if you use the certificate-based two-way authentication.


## Using the MQTT Protocol Directly

You can connect device to the EnOS Cloud using the MQTT protocol directly. In the CONNECT packet of the device should use the following values:


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
   + The value of the _deviceKey_ and _productKey_ can be found in the EnOS Console>.
 - For the **mqttPassword** field:
   + The value of the _deviceSecret_ can be found in the EnOS Console.
   + _content_ is consistent of the _productKey_, _deviceKey_, _timestamp_, and _clientID_. The value must be sorted in alphabetical order and concatenated without concatenation symbols.  
     Below is an example of _content_ when clientId=123, deviceKey=test, productKey=123, timestamp=1524448722000, deviceSecret=deviceSecret.
     ```
     sign= toUpperCase(hmacsha1(clientId123deviceKeytestproductKey123timestamp1524448722000deviceSecret))
     ```

     **NOTE**: The value of the timestamp must be same as the timestamp in _mqttClientID_.
