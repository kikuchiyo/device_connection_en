# Get Device Measuring Points

.. note:: Set the parameters according to the output and input parameters in the thing model.

After a device receives a get device measure points request, it returns the device measuring point in a reply message to EnOS cloud. You can get the information of the measuring points from the downstream.


Downstream
- Request TOPIC: `/sys/{productKey}/{deviceKey}/thing/service/measurepoint/get`

- Reply TOPIC: `/sys/{productKey}/{deviceKey}/thing/service/measurepoint/get_reply`

## Example Request Message

```
{
	"id": "123",
	"version": "1.0",
	"params": ["power", "temp"],
	"method": "thing.service.measurepoint.get"
}

```

## Example Response Message

```
{
	"id": "123",
	"code": 200,
	"data": {
		"power": "on",
		"temp": "23"
	}
}

```

## Parameter Description

.. list-table::
   :widths: 20 20 20 40

   * - Parameters
     - Type
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
     - List
     - Mandatory
     - Parameters used for getting the properties of the device measuring points.
   * - method
     - String
     - Mandatory
     - The method of the request.
   * - power
     - String
     - Optional
     - The identifier of the measuring point that you want to retrieve, in this example, the measuring point with the identifier of <strong>power</strong>.
   * - temp
     - String
     - Optional
     - The identifier of the measuring point that you want to retrieve, in this example, the measuring point with the identifier of <strong>temp</strong>.
   * - code
     - Integer
     - Mandatory
     - Response code &ldquo;200&rdquo; or the error code defined on the device end. &ldquo;200&rdquo; indicates that the request operation is executed successfully.
   * - data
     - JSON
     - Optional
     - Detailed returned information in JSON format.


<!--end-->
