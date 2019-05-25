# CoAP-based Connection and Communication

EnOS supports CoAP-based communication. The CoAP protocol is suitable for resource-limited and low-power devices, especially for NB-IoT devices. This topic describes the CoAP-based connection process on top of DTLS.

## Connection Process

The process for connecting NB-IoT devices to EnOS via CoAP is shown as follows:

.. image:: ../../../media/coap_connection_process.png

1. Obtain product key and product secret by creating a model and then a related product in EnOS.

2. Create a device in EnOS. For a device that uses unique-certificate-per-product authentication, obtain the device secret.
   
3. Configure the authentication keys on the device based on the authentication method you choose:
 - For unique-certificate-per-device authentication, configure product key, device key, and device secret. 
 - For unique-certificate-per-product authentication, configure product key and device key.
   
4. Power the device up and get the device online.

5. The device initiates a handshake request.

6. EnOS confirms the requests and completes the handshake. A secure message channel is established. 

7. (Optional) For devices that use unique-certificate-per-product, the device sends a request to EnOS to query the device secret.

8. (Optional) EnOS sends a response to the device with the device secret included in the response.

9.  The device uses product key, product secret and device secret to initiate authentication.

10. The device is authenticated and activated on EnOS.

11. EnOS sends a CoAP ACK message to the device.

## Before You Start

Depending on the authentication method, you need complete appropriate configurations in EnOS and obtain the required keys for authentication:
- For unique-certificate-per-device authentication, register devices one by one and obtain their `productKey`, `deviceKey` and `deviceSecret`. For information about how to register a device, see [Registering Devices](../../../howto/device/manage/creating_device).
- For unique-certificate-per-product authentication, create a product that the device belongs to and obtain the `productKey` and `productSecret` of the device. For information on how to create a product, see [Creating Products](../../../howto/device/manage/creating_device). For the devices authenticated with unique-certificate-per-product authentication, enable **Dynamic Registration** . For details, see [Managing Products](../../../howto/device/manage/managing_products).

For more information about device authentication, see [Security Authentication](../../../learn/deviceconnection_authentication).

## Connecting to the CoAP Server

The IP address of the CoAP server is `coap-<hostname>`, where `hostname` is where EnOS is located. For example, if EnOS is located on *abc.def.com*, then the CoAP server address would be *coap-abc.def.com*.

## Establishing the DTLS Secure Channel

The Pre-shared Key (PSK) is used as the key exchange algorithm to establish a secure channel. The Cipher Suites that EnOS CoAP server supports include the following:

- TLS-PSK-WITH-AES-128-CCM-8
- TLS-PSK-WITH-AES-128-CBC-SHA256

## Unique-certificate-per-device Authentication
  
The PSK used by devices during DTLS handshake is as follows:

```json
identity:{ProductKey},{DeviceKey},{SecureMode},{Lifetime}
Key:SHA-256({DeviceSecret}) Byte 9 to Byte 24 (16 bytes in total)
```

.. csv-table::
   :widths: auto

   "Parameter", "Description"
   "ProductKey", "Used for authentication."
   "DeviceKey",	"Used for authentication. It should be unique within an OU. You may use the IMEI of an NB-IoT device as its device key."
   "SecureMode", "SecureMode is set as 2 for unique-certificate-per-device authentication."
   "Lifetime", "Used to determine the online status of device. A device would be determined offline if it doesn't not exchange any message with EnOS within Lifetime. Lifetime is counted in seconds and the value range is 30 to 86400."
   "DeviceSecret",	"Used for authentication."

Sample PSK parameters:
```json
Identity: MuGsF6W4,15bBZlRknc,2,3600
Key:      0x01 0x24 0xDD 0xA7 0xA5 0xC6 0x3F 0x92 0xD9 0x8C 0x2F 0x80 0x9B 0x1E 0x3C 0x36
```

## Unique-certificate-per-product Authentication

The PSK used by devices during DTLS handshake is as follows:

```json
identity: {ProductKey},{DeviceKey},{SecureMode},{Lifetime}
Key: SHA-256({ProductSecret}) Byte 9 to Byte 24 (16 bytes in total)
```

.. csv-table::
   :widths: auto
   
   "Parameter", "Description"
   "ProductKey", "Used for authentication."
   "DeviceKey",	"Used for authentication. It should be unique within an OU. You may use the IMEI of an NB-IoT device as its device key."
   "SecureMode", "SecureMode is set as 3 for unique-certificate-per-device authentication."
   "Lifetime", "Used to determine the online status of device. A device would be determined offline if it doesn't not exchange any message with EnOS within Lifetime. Lifetime is counted in seconds and the value range is 30 to 86400."
   "ProductSecret", "Used for authentication."

Sample PSK parameters:
```json
Identity: MuGsF6W4,15bBZlRknc,3,3600
Key:      0x01 0x24 0xDD 0xA7 0xA5 0xC6 0x3F 0x92 0xD9 0x8C 0x2F 0x80 0x9B 0x1E 0x3C 0x36
 
```

After the handshake is completed, the device should query the device secret by sending a request. The request format is as follows:
`GET /topic/ext/session/{productKey}/{deviceKey}/thing/activate/info`

DeviceSecret is included in the response to this request:：

```json
Code: CoAP return code. Refer to CoAP protocol documentation.
Payload: {
    "id": {id},
    "version": "1.0",
    "method": "thing.activate.info",
    "params":{
        "assetId": {assetId},
        "productKey": {productKey},
        "deviceKey": {deviceKey},
        "deviceSecret": {deviceSecret}
    }
}
```

.. csv-table::
   :widths: auto
   
   "Parameter", "Description"
   "id", "The unique identifier of a message"
   "assetId", "Asset identifier of the device"
   
After `deviceSecret` is obtained, the device would be authenticated via `productKey`, `deviceKey` and `deviceSecret` when it tries to connect to EnOS.




 

 

