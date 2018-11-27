# Set device measure points

**Note:** Set the parameters according to the output and input parameters in the TSL model.

After a device receives a set device measure point request, it updates
the device measure points according to the request.

- TOPIC: /sys/{productKey}/{deviceKey}/thing/service/measurepoint/set

- Reply TOPIC: /sys/{productKey}/{deviceKey}/thing/service/measurepoint/set_reply

## Example request message

```
{
	"id": "123",
	"version": "1.0",
	"params": {
		"temperature": "30.5"
	},
	"method": "thing.service.measurepoint.set"
}

```

## Example response message

```
{
	"id": "123",
	"code": 200,
	"data": {}
}

```

## Parameter description

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
    <td>Parameters used for setting device properties. </td>
  </tr>
  <tr>
    <td>method</td>
    <td>String</td>
    <td>Mandatory</td>
    <td>The method of the request. </td>
  </tr>
  <tr>
    <td>temperature</td>
    <td>String</td>
    <td>Optional</td>
    <td>Property name.</td>
  </tr>
  <tr>
    <td>code</td>
    <td>Integer</td>
    <td>Mandatory </td>
    <td>Response code. &ldquo;200&rdquo; indicates the request is executed successfully. </td>
  </tr>
  <tr>
    <td>data</td>
    <td>String</td>
    <td>Optional </td>
    <td>Detailed information, in JSON format. </td>
  </tr>
</table>
