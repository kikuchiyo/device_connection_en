# Set Device Measuring Points

**Note:** Set the parameters according to the output and input parameters in the thing model.

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

<table>
  <tr>
    <th>Parameters</th>
    <th>Type</th>
    <th>Occurrence </th>
    <th>Description</th>
  </tr>
  <tr>
    <td>id</td>
    <td>Long</td>
    <td>Optional </td>
    <td>Message ID. Reserved for future use.</td>
  </tr>
  <tr>
    <td>version</td>
    <td>String</td>
    <td>Mandatory </td>
    <td>Version of the protocol. Current version is 1.0. </td>
  </tr>
  <tr>
    <td>params</td>
    <td>Object</td>
    <td>Mandatory </td>
    <td>Parameters used for setting the value of the measuring point of the device. </td>
  </tr>
  <tr>
    <td>method</td>
    <td>String</td>
    <td>Mandatory</td>
    <td>The method of the request. </td>
  </tr>
  <tr>
    <td>temperature</td>
    <td>Float</td>
    <td>Optional</td>
    <td>The identifier of the measuring point that you want to modify, in this example, the measuring point with the identifier of <strong>temperature</strong>. The value you set must match the data type defined for this measure point.​ For example, when the data type of this parameter is set to float in the model, the value here must be a float.</td>
  </tr>
  <tr>
    <td>code</td>
    <td>Integer</td>
    <td>Mandatory </td>
    <td>Response code &ldquo;200&rdquo; or the error code defined on the device end. &ldquo;200&rdquo; indicates that the request operation is executed successfully. </td>
  </tr>
  <tr>
    <td>data</td>
    <td>String</td>
    <td>Optional </td>
    <td>Detailed returned information in JSON format. </td>
  </tr>
</table>
