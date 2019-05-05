# Setting Measure Points and Invoking Services (Non-DTLS)

Applications can use EnOS open APIs to set measurepoints or invoke services for the devices connected via CoAP. The process is as follows:

.. image:: ../../../media/coap_downstream_flow_non_dtls.png

For more information about the data formats of the request and response, and parameter description, see [Sending Commands to Devices (Pass-through)](../../mqtt/downstream/devices/invoke_services_pass).

When the application calls an API to set measurepoints or invoke services from a device, EnOS caches this request. When a device sends a request to EnOS, EnOS will include the request sent by the application in the response to the device's request, in the form of an Option (2100) that is EnOS-defined.

Format of the response sent to the device by EnOS is as follows:

```json
Code: CoAP return code
Payload: {RequestPayload}
Customized Option 2100:/topic/sys/${ProductKey}/${DeviceKey}/thing/model/down_raw
``` 

In this response:

.. csv-table::
   :widths: auto

   "Parameter", "Description"
   "ProductKey", "Used for authentication."
   "DeviceKey",	"Used for authentication."
   "Payload", "The payload requested by the device."

The device sends a request to query services after the device receives the response with option. The format of the request is as follows:

 ```json
GET /topic/sys/${ProductKey}/${DeviceKey}/thing/model/down_raw
Customized Option 2101: ${Sign}
```
.. note:: `${Sign}` is generated in the following procedure:
 1. Concatenate the following fields in the following order:` token${Token}sequence${Sequence}`
     `${Token}` is the token assigned to the device when it is authenticated by EnOS. `${Sequence}` is positive int which indicates the order of messages a device sends to EnOS in a session. The first message in a session has a sequence value of 1. `${Sequence}` must be larger than the sequence of the last message the device sent to EnOS. If the device loses the sequence of the last message it sends to EnOS, it must re-initiate authentication.

 2. Generate `${SignKey}` by extracting Byte 9 to Byte 24 from the SHA-256 hash of `${DeviceSecret}`. The lenght of `${SignKey}` is 16 bytes.

 3. Calculate the AES-128 hash of `${SignKey}` and `token${Token}sequence${Sequence}`

 4. Capitalize the letters in the calculated hash.

The response of EnOS to the previous request is as follows:

```json
Code: CoAP return code
Payload: ${Payload}
```

If more services are invoked, EnOS include those requests in later responses as Option (2100). The device repeats querying the services that are invoked.

After the device completes the invoked service or measure point setting, it sends the execution result to EnOS based on the topic and parameter specifications defined by EnOS.