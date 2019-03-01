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
  mqttPassword: uppercase(sign_hmac(<content><deviceSecret>))
```

- For the **mqttClientId** segment:

  - _clientId_: Mandatory. Can be specified using either the MAC address or device serial number. It must contain no more than 64 characters. The parameters within  ``||`` are the optional parameters.
  - _securemode_: Optional. Indicates the secure mode that has been used. Currently, only support `securemode=2`.
  - _signmethod_: Optional. Indicates the signing method. Currently, only support `signmethod=hmacsha1`.
  - _timestamp_: Optional. Indicates the current time in milliseconds.

- For the **mqttUsername** segment:

  - The value of the _deviceKey_ and _productKey_ of a device that can be obtained from the EnOS Console after you complete provisioning the device.

- For the **mqttPassword** segment:

  - _content_: The concatenation of _clientID_, _deviceKey_, _productKey_, _timestamp_, and their values. The parameter names must be sorted in alphabetical order and concatenated without concatenation symbols.  
  - _deviceSecret_: The value of the _deviceSecret_ that can be obtained from the EnOS Console. The value of _deviceSecret_ follows the _content_ without any space or symbol.

    Below is an example of _mqttPassword_ when _clientId_=`123`, _deviceKey_=`test`, _productKey_=`123`, _timestamp_=`1524448722000`, _deviceSecret_=`aaabbbcc123`.

    ```
    sign=uppercase(hmacsha1(clientId123deviceKeytestproductKey123timestamp1524448722000aaabbbcc123))
    ```

.. note:: The value of `timestamp` must be same as the `timestamp` in the **mqttClientId** segment.


<!--end-->
