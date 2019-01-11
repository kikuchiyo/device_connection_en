# Set Device Measuring Points

.. note:: Set the parameters according to the output and input parameters in the thing model.

After a device receives a set device measuring point request, it updates the value of the measuring points of the device according to the request.

Downstream
- Request TOPIC: `/sys/{productKey}/{deviceKey}/thing/service/measurepoint/set`

- Reply TOPIC: `/sys/{productKey}/{deviceKey}/thing/service/measurepoint/set_reply`

## Example Request Message

```
{
	"id": "123",
	"version": "1.0",
	"params": {
		"temperature": 30.5
	},
	"method": "thing.service.measurepoint.set"
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
     - Message ID. Reserved for future use.
   * - version
     - String
     - Mandatory
     - Version of the protocol. Current version is 1.0.
   * - params
     - Object
     - Mandatory
     - Parameters used for setting the value of the measuring point of the device.
   * - method
     - String
     - Mandatory
     - The method of the request.
   * - temperature
     - Float
     - Optional
     - The identifier of the measuring point that you want to modify, in this example, the measuring point with the identifier of temperature. The value you set must match the data type defined for this measure point.​ For example, when the data type of this parameter is set to float in the model, the value here must be a float.
   * - code
     - Integer
     - Mandatory
     - Response code &ldquo;200&rdquo; or the error code defined on the device end. &ldquo;200&rdquo; indicates that the request operation is executed successfully.
   * - data
     - String
     - Optional
     - Detailed returned information in JSON format.

<!--end-->
