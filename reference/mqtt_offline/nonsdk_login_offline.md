# Establishing Connection with EnOS Cloud using the MQTT Protocol

This article instructs how to establish connection from 3rd-party systems to the EnOS Cloud through the MQTT protocol.

The supported MQTT version:

- MQTT v3.1.1 on port 11883 if you use the secret-based one-way authentication.
- MQTT v3.1.1 over SSL/TLS on port 18883 if you use the certificate-based two-way authentication.


## Using the MQTT Protocol Directly

You can connect 3rd-party systems to the EnOS by using the MQTT protocol directly. Include the following values in the CONNECT packet of the device:

```
  mqttClientId: clientId+"|securemode=<securemode>,signmethod=sha1,timestamp=132323232|"
  mqttUsername: deviceKey+"&"+productKey
  mqttPassword: uppercase(sign_hmac(<content><deviceSecret>))
```
- For the **mqttClientId** segment:

  - _clientId_: Required. Can be specified by using either the MAC address or device serial number. It must contain no more than 64 characters. The parameters within  ``||`` are the required parameters. 
  - _securemode_: Required. Indicates the secure mode that has been used. Supports only `securemode=2`.
  - _signmethod_: Required. Indicates the signing method. Currently, only support `signmethod=sha1`.
  - _timestamp_: Required. Indicates the current time in milliseconds.

- For the **mqttUsername** segment:

  - The value of the _deviceKey_ and _productKey_ of a device that can be obtained from the EnOS Console after you complete registering the device.

- For the **mqttPassword** segment:

  <!-- - You can use the [Password Generation Tool](../../_static/nonsdk_enosmqttsign_index.html) to generate the password quickly.-->

  - _content_: The concatenation of _clientID_, _deviceKey_, _productKey_, _timestamp_, and their values. The parameter names must be sorted in alphabetical order and concatenated without concatenation symbols.  

  - _deviceSecret_: When the device carries the device secret, append the value of _deviceSecret_ after _content_ without any space or symbol.

    Below is an example of _mqttPassword_ when _clientId_=`123456`, _deviceKey_=`tPbZGCdmaE`, _productKey_=`KV315idW`, _timestamp_=`1548753362502`, _deviceSecret_=`M3yy874uGY8INjEGddTR`.

    ```
    sign=uppercase(sha1(clientId123456deviceKeytPbZGCdmaEproductKeyKV315idWtimestamp1548753362502M3yy874uGY8INjEGddTR))
    ```

.. note:: The value of `timestamp` must be same as the `timestamp` in the **mqttClientId** segment.


<!--end-->
