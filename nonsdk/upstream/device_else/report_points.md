# Report Device Measure Points

A device can publish a message to this topic to report the newly added measure point to the cloud.

**Note:** Configure the parameters according to the output and input parameters of the measure points.

Upstream
- Request TOPIC: `/sys/{productKey}/{deviceKey}/thing/measurepoint/post`

- Reply TOPIC: `/sys/{productKey}/{deviceKey}/thing/measurepoint/post_reply`

## Example Request Message

```
{
	"id": "123",
	"version": "1.0",
	"params": {
		"measurepoints": {
			"Power": {
				"value": 1.0,
				"quality": 9
			},
			"temp": 1.02,
			"branchCurr": [
				"1.02", "2.02", "7.93"
			]
		},
		"time": 123456
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
    <td>List of the measure point-type of features of the device.</td>
  </tr>
  <tr>
    <td>power</td>
    <td>-</td>
    <td>Optional</td>
    <td>The identifier of the measure point that you want to report, in this example, the event with the identifier of <strong>power</strong>.The value you set must match the data type defined for this parameter. For example, when the quality indicator is selected, the data here must be <strong>value</strong> and <strong>quality</strong>. </td>
  </tr>
  <tr>
    <td>value</td>
    <td>Integer</td>
    <td>Optional</td>
    <td>The parameter name of the quality indicator of this measure point, in this example, the parameter named <strong>value</strong>. The value you set must match the data type defined for this parameter. For example, when the data type of this parameter is set to integer in the model, the value here must be an integer.</td>
  </tr>
  <tr>
    <td>quality</td>
    <td>Integer</td>
    <td>Optional</td>
    <td>The parameter name of the quality indicator of this measure point, in this example, the <strong>quality</strong> parameter that indicates the data quality. The valid value is integer in the range 0 - 9.</td>
  </tr>
  <tr>
    <td>temp</td>
    <td>Integer</td>
    <td>Optional</td>
    <td>The identifier of the measure point that you want to report, in this example, the measure point with the identifier of <strong>temp</strong>. Similar to above, the value you set must match the data type defined for this parameter.</td>
  </tr>
  <tr>
    <td>branchCurr</td>
    <td>Array</td>
    <td>Optional</td>
    <td>The identifier of the measure point that you want to report, in this example, the measure point with the identifier of <strong>branchCurr</strong>. Similar to above, the value you set must match the data type defined for this parameter.</td>
  </tr>
  <tr>
    <td>time</td>
    <td>Timestamp</td>
    <td>Optional</td>
    <td>The timestamp for this request topic. When not specified, the value is the server time.</td>
  </tr>
  <tr>
    <td>code</td>
    <td>Integer</td>
    <td>Mandatory</td>
    <td>Response code. &ldquo;200&rdquo; indicates that the request operation is executed successfully. </td>
  </tr>
  <tr>
    <td>data</td>
    <td>JSON</td>
    <td>Optional</td>
    <td>Detailed returned information in JSON format.</td>
  </tr>
</table>
