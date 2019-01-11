# Invoke Device Services (Non-Passthrough)

Device receives the invoke services request through the topic. EnOS Cloud publishes a message to the device topic to invoke the device services.

Downstream
- Request TOPIC: `/sys/{productKey}/{deviceKey}/thing/service/{tsl.service.identifier}`

- Reply TOPIC: `/sys/{productKey}/{deviceKey}/thing/service/{tsl.service.identifier}_reply`


.. note:: `tsl.service.identifier` is the identifier of the service that has been defined in the thing model.


## Example Request Message

```
{
	"id": "123",
	"version": "1.0",
	"params": {
		"Power": "on",
		"WindState": 2
	},
	"method": "thing.service.{tsl.service.identifier}"
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
     - Type​
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
     - Parameters used for invoking device services.
   * - method
     - String
     - Mandatory
     - The method of this request.
   * - Power
     - String
     - Optional
     - The identifier of the service that you want to invoke, in this example, the service with the identifier of **Power**.The value you set must match the data type defined for this parameter. For example, when the data type of this parameter is set to string in the model, the value here must be a string.
   * - WindState
     - Integer
     - Optional
     - The identifier of the service that you want to invoke, in this example, the event with the identifier of **WindState**. Similar to above, the value you set must match the data type defined for this parameter.​
   * - code
     - Integer
     - Mandatory
     - Response code &ldquo;200&rdquo; or the error code defined on the device end. &ldquo;200&rdquo; indicates that the request operation is executed successfully.
   * - data
     - JSON
     - Optional
     - Detailed returned information in JSON format.

<!--end-->
