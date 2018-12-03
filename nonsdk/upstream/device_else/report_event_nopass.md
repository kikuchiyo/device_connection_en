# Report Device Events​ (non-passthrough)

If non-passthrough mode is used, the device generates data in the JSON
format and then sends the data to EnOS Cloud.

Upstream
- Request TOPIC: /sys/{productKey}/{deviceKey}/thing/event/{tsl.event.identifier}/post

- Reply TOPIC: /sys/{productKey}/{deviceKey}/thing/event/{tsl.event.identifier}/post_reply

## Example Request Message

```
{
  "id": "123",
  "version": "1.0",
 "params": {
		"events": {
			"Power": {
				"value": "1.0",
				"quality": "9"
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
    <td>Parameters</td>
    <td>Type</td>
    <td>Occurrence </td>
    <td>Description</td>
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
    <td>Version of the protocol. Current version is   1.0.</td>
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
    <td>Events of the device.</td>
  </tr>
  <tr>
    <td>power</td>
    <td>String</td>
    <td>Optional</td>
    <td>The property of the events.</td>
  </tr>
  <tr>
    <td>value</td>
    <td>String</td>
    <td>Optional</td>
    <td>The property of the events.</td>
  </tr>
  <tr>
    <td>quality</td>
    <td>String</td>
    <td>Optional</td>
    <td>The property of the events.</td>
  </tr>
  <tr>
    <td>temp</td>
    <td>String</td>
    <td>Optional</td>
    <td>The property of the events.</td>
  </tr>
  <tr>
    <td>branchCurr</td>
    <td>String</td>
    <td>Optional</td>
    <td>The property of the events.</td>
  </tr>
  <tr>
    <td>time</td>
    <td>String</td>
    <td>Optional</td>
    <td>Timestamp for reporting measure point. If leave   it blank, the value is set to the timestamp of the server.</td>
  </tr>
  <tr>
    <td>method</td>
    <td>String</td>
    <td>Optional</td>
    <td>The method of the request.</td>
  </tr>
  <tr>
    <td>temperature</td>
    <td>String</td>
    <td>Mandatory</td>
    <td>Property name.</td>
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
    <td>Optional</td>
    <td>Detailed information, in JSON format.</td>
  </tr>
</table>
