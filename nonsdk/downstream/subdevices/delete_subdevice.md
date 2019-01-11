# Delete Sub-devices

This TOPIC notifies the edge that the specific sub-device belongs to this edge have been deleted from EnOS Cloud. EnOS Cloud publishes
the delete devices message to the edge asynchronously.

Downstream
- Request TOPIC: `/ext/session/{productKey}/{deviceKey}/combine/delete`

- Reply TOPIC: `/ext/session/{productKey}/{deviceKey}/combine/delete_reply`

.. note:: The *productKey* and *deviceKey* in the TOPIC are the credentials of the edge.

## Example Request Message

```
{
	"id": "123",
	"version": "1.0",
	"params": [
            {
		"productKey": "xxx",
		"deviceKey": "xxx"
	}
	],
	"method": "combine.delete"
}
```

## Example Response Message

```
{
	"id": "123",
	"code": 200,
	"data": {}
}

```

## Parameter Description​

.. list-table::
   :widths: 20 20 20 40

   * - Parameters
     - ​Type​
     - Occurrence
     - Description
   * - id
     - Long
     - Optional
     - Message ID. Reserved parameter for future use.
   * - version
     - String
     - Mandatory
     - Version of the protocol. Current version is 1.0.
   * - params
     - Object
     - Mandatory
     - Parameters used for deleting a sub-device.
   * - productKey
     - String
     - Mandatory
     - Product Key of the sub-device.
   * - deviceKey
     - String
     - Mandatory
     - Device key of the sub-device.
   * - method
     - String
     - Mandatory
     - The method of the request.
   * - code
     - String
     - Mandatory
     - Response code &ldquo;200&rdquo; or the error code defined on the device end. &ldquo;200&rdquo; indicates that the request operation is executed successfully.
   * - data
     - JSON
     - Optional
     - Detailed returned information in JSON format.

<!--end-->
