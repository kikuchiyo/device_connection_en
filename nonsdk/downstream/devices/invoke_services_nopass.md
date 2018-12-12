# Invoke Device Services (Non-Passthrough)

Device receives the invoke services request through the topic. EnOS Cloud publishes a message to the device topic to invoke the device services.

Downstream
- Request TOPIC: `/sys/{productKey}/{deviceKey}/thing/service/{tsl.service.identifier}`

- Reply TOPIC: `/sys/{productKey}/{deviceKey}/thing/service/{tsl.service.identifier}_reply`


**Note:** ``tsl.service.identifier`` is the identifier of the service that has been defined in the thing model.


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

<table>
  <tr>
    <th>Parameters</th>
    <th>Type​</th>
    <th>Occurrence </th>
    <th>Description</th>
  </tr>
  <tr>
    <td>id</td>
    <td>Long</td>
    <td>Optional </td>
    <td>Message ID. Reserved parameter for future use.</td>
  </tr>
  <tr>
    <td>version</td>
    <td>String</td>
    <td>Mandatory </td>
    <td>Version of the protocol. Current version is 1.0. </td>
  </tr>
  <tr>
    <td>params</td>
    <td>List</td>
    <td>Mandatory </td>
    <td>Parameters used for invoking device services. </td>
  </tr>
  <tr>
    <td>method</td>
    <td>String</td>
    <td>Mandatory</td>
    <td>The method of this request.</td>
  </tr>
  <tr>
    <td>Power</td>
    <td>String</td>
    <td>Optional </td>
    <td>The identifier of the service that you want to invoke, in this example, the service with the identifier of <strong>Power</strong>.The value you set must match the data type defined for this parameter. For example, when the data type of this parameter is set to string in the model, the value here must be a string.</td>
  </tr>
  <tr>
    <td>WindState</td>
    <td>Integer</td>
    <td>Optional </td>
    <td>The identifier of the service that you want to invoke, in this example, the event with the identifier of <strong>WindState</strong>. Similar to above, the value you set must match the data type defined for this parameter.​</td>
  </tr>
  <tr>
    <td>code</td>
    <td>Integer</td>
    <td>Mandatory </td>
    <td>Response code &ldquo;200&rdquo; or the error code defined on the device end. &ldquo;200&rdquo; indicates that the request operation is executed successfully.</td>
  </tr>
  <tr>
    <td>data</td>
    <td>JSON</td>
    <td>Optional </td>
    <td>Detailed returned information in JSON format. </td>
  </tr>
</table>
