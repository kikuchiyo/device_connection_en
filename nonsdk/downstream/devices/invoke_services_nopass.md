# Invoke device services (non-passthrough)

Device receives the invoke service request through the topic. EnOS Cloud
publishes a message to the device topic to invoke the device services.

Downstream
- TOPIC: /sys/{productKey}/{deviceKey}/thing/service/{tsl.service.identifier}

- Reply TOPIC: /sys/{productKey}/{deviceKey}/thing/service/{tsl.service.identifier}_reply

## Example request message

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

## Example response message

```
{
	"id": "123",
	"code": 200,
	"data": {}
}
```

## Parameter description​

<table>
  <tr>
    <td>Parameters</td>
    <td>Type​</td>
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
    <td>Parameters used for invoking device services. </td>
  </tr>
  <tr>
    <td>method</td>
    <td>String</td>
    <td>Mandatory</td>
    <td>The method of the request. </td>
  </tr>
  <tr>
    <td>Power</td>
    <td>String</td>
    <td>Optional </td>
    <td>Parameter   name of the service.​</td>
  </tr>
  <tr>
    <td>WindState</td>
    <td>String</td>
    <td>Optional </td>
    <td>Parameter   name of the service.​</td>
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
    <td>Detailed information , in JSON format. </td>
  </tr>
</table>

**Note:** ``tsl.service.identifier`` is the identifier of the service that
has been defined in the TSL model.
