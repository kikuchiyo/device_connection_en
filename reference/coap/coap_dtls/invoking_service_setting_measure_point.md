# Setting Measure Points and Invoking Services 

Applications can use EnOS open APIs to set measurepoints or invoke services for the devices connected via CoAP. The process is as follows:

.. image:: ../../../media/coap_downstream_flow.png

For more information about the data formats of the request and response, and parameter description, see [Sending Commands to Devices (Pass-through)](../../mqtt/downstream/devices/invoke_services_pass).

When the application calls an API to set measurepoints or invoke services from a device, EnOS caches this request. When a device sends a request to EnOS, EnOS will include the request sent by the application in the response to the device's request, in the form of an Option (2100) that is EnOS-defined.

Format of the response sent to the device by EnOS:

```json
Code: CoAP return code
Payload: {RequestPayload}
Customized Option 2100: /topic/{RequestTopic}
``` 

The application sends a request to invoke services after the device receives the response with option.

Format of the request to query the invoked service is as follows:
 `GET /topic/{RequestTopic}`

Response to the previous request:

```json
Code: CoAP return code
Payload: 
```

If there are more services to be invoked, EnOS will also include the option (2100) in the responses. And the device will repeat sending request to query the service invoked.

After measure points are set or services are invoked, the device sends the execution results to EnOS to the response topic and in the data format prescribed by EnOS. 
