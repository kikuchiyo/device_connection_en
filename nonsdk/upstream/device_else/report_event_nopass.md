# Report Device Events​ (Non-Passthrough)


A device can publish a message to this topic to report the newly added event to the cloud.

If non-passthrough mode is used, the device data sent to the cloud is in JSON.

Upstream
- Request TOPIC: `/sys/{productKey}/{deviceKey}/thing/event/{tsl.event.identifier}/post`

- Reply TOPIC: `/sys/{productKey}/{deviceKey}/thing/event/{tsl.event.identifier}/post_reply`

**Note:** ``tsl.service.identifier`` is the identifier of the event that has been defined in the thing model.



## Example Request Message

```
{
  "id": "123",
  "version": "1.0",
 "params": {
	"events": {
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
  "method": "thing.event.{tsl.event.identifier}.post"
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
    <td>Optional</td>
    <td>Message ID. Reserved parameter for future use.</td>
  </tr>
  <tr>
    <td>version</td>
    <td>String</td>
    <td>Mandatory</td>
    <td>Version of the protocol. Current version is 1.0.</td>
  </tr>
  <tr>
    <td>params</td>
    <td>Object</td>
    <td>Mandatory</td>
    <td>Parameters used for reporting device events.</td>
  </tr>
  <tr>
    <td>events</td>
    <td>Object</td>
    <td>Mandatory</td>
    <td>List of the event-type of features of the device.</td>
  </tr>
  <tr>
    <td>power</td>
    <td>String</td>
    <td>Optional</td>
    <td>The identifier of the event that you want to report, in this example, the event with the identifier of <strong>power</strong>. </td>
  </tr>
  <tr>
    <td>value</td>
    <td>Integer</td>
    <td>Optional</td>
    <td>The name of the output parameter of this event, in this example, the parameter named <strong>value</strong>. The value you set must match the data type defined for this parameter. For example, when the data type of this parameter is set to integer in the thing model, the value here must be an integer. </td>
  </tr>
  <tr>
    <td>quality</td>
    <td>Integer</td>
    <td>Optional</td>
    <td>The name of the output parameter of this event, in this example, the <strong>quality</strong> parameter that indicates the data quality. The valid value is integer in the range 0 - 9.</td>
  </tr>
  <tr>
    <td>temp</td>
    <td>Integer</td>
    <td>Optional</td>
    <td>The identifier of the event that you want to report, in this example, the event with the identifier of <strong>temp</strong>. Similar to above, the value you set must match the data type defined for this parameter.</td>
  </tr>
  <tr>
    <td>branchCurr</td>
    <td>Array</td>
    <td>Optional</td>
    <td>The identifier of the event that you want to report,  in this example, the event with the identifier of <strong>branchCurr</strong>. Similar to above, the value you set must match the data type defined for this parameter.</td>
  </tr>
  <tr>
    <td>time</td>
    <td>String</td>
    <td>Optional</td>
    <td>The timestamp of this request. When not specified, the value is the server time.</td>
  </tr>
  <tr>
    <td>method</td>
    <td>String</td>
    <td>Optional</td>
    <td>The method of the request.</td>
  </tr>
  <tr>
    <td>code</td>
    <td>Integer</td>
    <td>Mandatory</td>
    <td>Response code. &ldquo;200&rdquo; indicates that the requested operation is executed successfully. </td>
  </tr>
  <tr>
    <td>data</td>
    <td>JSON</td>
    <td>Optional</td>
    <td>Detailed returned information in JSON format.</td>
  </tr>
</table>
