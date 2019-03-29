# Establishing Connection with EnOS Cloud using the MQTT Protocol

This article instructs how to establish connection from devices to the EnOS Cloud through the MQTT protocol.

The supported MQTT version:

- MQTT v3.1.1 on port 11883 if you use the secret-based one-way authentication.
- MQTT v3.1.1 over SSL/TLS on port 18883 if you use the certificate-based two-way authentication.


## Using the MQTT Protocol Directly

You can connect devices to the EnOS Cloud using the MQTT protocol directly. Include the following values in the CONNECT packet of the device:

```
  mqttClientId: clientId+"|securemode=<securemode>,signmethod=hmacsha1,timestamp=132323232|"
  mqttUsername: deviceKey+"&"+productKey
  mqttPassword: toUpperCase(hmacsha1(content+deviceSecret/productSecret))
```
- For the **mqttClientId** segment:

  - _clientId_: Mandatory. Identifier of the device, `deviceKey`. Can be specified using either the MAC address or device serial number. It must contain no more than 64 characters. The parameters within  ``||`` are the optional parameters. 
  - _securemode_: Optional. Indicates the secure mode that has been used. 
    - For secret-per-device authentication (`productKey`, `deviceKey`, `deviceSecret` is provided to statically activate the device), the value is `2`.
    - For secret-per-product authentication (`productKey`, `productSecret`, `deviceKey` is provided to dynamically activate the device) the value is `3`.
  - _signmethod_: Optional. Indicates the signing method. Currently, only support `signmethod=hmacsha1`.
  - _timestamp_: Optional. Indicates the current time in milliseconds.

- For the **mqttUsername** segment:

  - The value of the _deviceKey_ and _productKey_ of a device that can be obtained from the EnOS Console after you complete registering the device.

- For the **mqttPassword** segment:

  - _content_: The concatenation of _clientID_, _deviceKey_, _productKey_, _timestamp_, and their values. The parameter names must be sorted in alphabetical order and concatenated without concatenation symbols.  
  - _deviceSecret_: When the device carries the device secret, append the value of _deviceSecret_ after _content_ without any space or symbol.
   
       Below is an example of _mqttPassword_ when _clientId_=`123`, _deviceKey_=`test`, _productKey_=`123`, _timestamp_=`1524448722000`, _deviceSecret_=`deviceSecretxxx`.

    ```
    mqttPassword = toUpperCase(hmacsha1(clientId123deviceKeytestproductKey123timestamp1524448722000deviceSecretxxx))
    ```
  - _productSecret_: When the device carries the product secret, append the value of the _productSecret_ after _content_ without any space or symbol.

    Below is an example of _mqttPassword_ when _clientId_=`123`, _deviceKey_=`test`, _productKey_=`123`, _timestamp_=`1524448722000`, productSecret=`productSecretxxx`.

    ```
    mqttPassword = toUpperCase(hmacsha1(clientId123deviceKeytestproductKey123timestamp1524448722000productSecretxxx))
    ```

Only unactivated device can be authenticated via product secret, the `productKey`, `productSecret`, and `deviceKey` is written into the device to dynamically obtain the `deviceSecret` upon first attempt to connect to EnOS Cloud. The device is then activated through its device triple and starts to transmit data to the cloud. This is called _dynamic activate_ of a device.

When you perform the device-end development, you need to persist the device triple in the device. After being activated, a device is signed through its `deviceSecret`. To re-activate a device, you must delete the device from the EnOS Console and re-register the device.

In the dynamic activation mode, the `deviceScret` is returned to the device after the device logs in through the following topic:
```
/ext/session/{productKey}/{deviceKey}/thing/activated/info
```
And the returned message takes the following format:
```
{
    "id": "1",
    "version": "1.0",
    "method": "thing.activate.info",
    "params":{
        "assetId": "12344",
        "productKey": "1234556554",
        "deviceKey": "deviceKey1234",
        "deviceSecret": "xxxxxx"
    }
}
```

You'll need to handle the message returned upon dynamic activation, the following shows a sample for Java.

```
 client.setArrivedMsgHandler(DeviceActivateInfoCommand.class, (DeviceActivateInfoCommand msg,  List<String> args) -> {
            //try persist the reply device info and then rebuild the mqttClient
            System.out.println(msg.getDeviceInfo());
            return null;
        });
```

.. note:: The value of `timestamp` must be same as the `timestamp` in the **mqttClientId** segment.


<!--end-->
