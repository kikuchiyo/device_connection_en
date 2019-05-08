# Reporting Attributes, Measure points and Events to EnOS

Devices connected to EnOS through CoAP can report attribute values, measure points, and events to EnOS. The process is as follows:

.. image:: ../../../media/coap_upstream_flow.png

The data transmitted by the low-power devices connected via CoAP are often binary. These data can be passed through to EnOS and then converted to EnOS-defined JSON by using the parsing script.

When a device is connected to EnOS via CoAP, the topic specifications are consistent with those of MQTT. For more information about the request data formats, response data formats and parameter descriptions for upstream messages, see [Reporting Attributes, Measurepoints and Events from Devices (Pass-through)](../../mqtt/upstream/device_else/report_event_pass).

In addition to the payload defined by EnOS device protocol specifications, the response also includes CoAP return codes. The structure of return codes and response data are given as follows:

```json
Code: return code defined by CoAP protocol
Payload: {ResponsePayload}
``` 

The return codes defined by CoAP protocol are illustrated as follows:

.. csv-table::
   :widths: auto

   "Return code", "Definition", "Payload", "Description"
   "2.04", "Changed", "Response data supported by EnOS", "Correct request"
   "4.00", "Bad Request", "None", "Payload sent by the request is illegal"
   "4.01", "Unauthorized", "None", "Unauthorized request"
   "4.03", "Forbidden", "None, "Forbidden request"
   "4.04", "Not Found", "None", "The path requested does not exist"
   "4.05", "Method Not Allowed", "None", "Request method is illegal"
   "5.00", "Internal Server Error", "None", "EnOS internal error"

<!--end-->
