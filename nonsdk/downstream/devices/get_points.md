# Get Device Measuring Points

**Note:** Set the parameters according to the output and input parameters in the TSL model.


After a device receives a get device measure points request, it returns
the device measuring point in a reply message to EnOS cloud. You can get
the information of the measure points from the the downstream.


Downstream
- Request TOPIC: /sys/{productKey}/{deviceKey}/thing/service/measurepoint/get

- Reply TOPIC: /sys/{productKey}/{deviceKey}/thing/service/measurepoint/get_reply

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

<table>
  <tr>
    <td>Parameters</td>
    <td>Type</td>
    <td>Occurrence </td>
    <td>Description</td>
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
    <td>Parameters used for getting device properties. </td>
  </tr>
  <tr>
    <td>method</td>
    <td>String</td>
    <td>Mandatory</td>
    <td>The method of the request. </td>
  </tr>
  <tr>
    <td>power</td>
    <td>String</td>
    <td>Optional </td>
    <td>Property name.</td>
  </tr>
  <tr>
    <td>temp</td>
    <td>String</td>
    <td>Optional </td>
    <td>Property name.</td>
  </tr>
  <tr>
    <td>code</td>
    <td>Integer</td>
    <td>Mandatory </td>
    <td>​ Response code &ldquo;200&rdquo; or the error code defined on device end. &ldquo;200&rdquo; indicates the request is executed successfully. </td>
  </tr>
  <tr>
    <td>data </td>
    <td>String </td>
    <td>Optional </td>
    <td>Detailed information, in JSON format. </td>
  </tr>
</table>
