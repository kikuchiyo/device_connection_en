# Report Device Measuring points

**Note:** Configure the parameters according to the output and input parameters of the measuring points.

Upstream
- Request TOPIC: /sys/{productKey}/{deviceKey}/thing/measurepoint/post

- Reply TOPIC: /sys/{productKey}/{deviceKey}/thing/measurepoint/post_reply

## Example Request Message

```
{
	"id": "123",
	"version": "1.0",
	"params": {
		"measurepoints": {
			"Power": {
				"value": "1.0",
				"quality": "9"
			},
			"temp": 1.02,
			"branchCurr": [
				"1.02", "2.02", "7.93"
			]
		}
		"time": 123456
	}
},
"method": "thing.measurepoint.post"
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
    <td>Mandatory</td>
    <td>Version of the protocol. Current version is 1.0. </td>
  </tr>
  <tr>
    <td>params</td>
    <td>Object</td>
    <td>Mandatory</td>
    <td>Parameters used for reporting device measure points. </td>
  </tr>
  <tr>
    <td>method</td>
    <td>String</td>
    <td>Mandatory</td>
    <td>The method of the device.</td>
  </tr>
  <tr>
    <td>measurepoints</td>
    <td>Object</td>
    <td>Mandatory</td>
    <td>Measure point of the device.</td>
  </tr>
  <tr>
    <td>power</td>
    <td>String</td>
    <td>Optioanl</td>
    <td>The property of this measure point.</td>
  </tr>
  <tr>
    <td>value</td>
    <td>String</td>
    <td>Optioanl</td>
    <td>The property of this measure point.</td>
  </tr>
  <tr>
    <td>quality</td>
    <td>Strign</td>
    <td>Optioanl</td>
    <td>The property of this measure point.</td>
  </tr>
  <tr>
    <td>temp</td>
    <td>String</td>
    <td>Optioanl</td>
    <td>The property of this measure point.</td>
  </tr>
  <tr>
    <td>branchCurr</td>
    <td>String</td>
    <td>Optioanl</td>
    <td>The property of this measure point.</td>
  </tr>
  <tr>
    <td>time</td>
    <td>Timestamp</td>
    <td>Optioanl</td>
    <td>Timestamp for reporting measure point. If leave   it blank, the value is set to the timestamp of the server.</td>
  </tr>
  <tr>
    <td>code</td>
    <td>Integer</td>
    <td>Mandatory</td>
    <td>Response code. &ldquo;200&rdquo; indicates the request is executed successfully. </td>
  </tr>
  <tr>
    <td>data</td>
    <td>String</td>
    <td>Optional </td>
    <td>Detailed information, in JSON format.</td>
  </tr>
</table>
