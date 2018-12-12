# Delete Sub-devices

This TOPIC notifies the edge that the specific sub-device belongs to this edge have been deleted from EnOS Cloud. EnOS Cloud publishes
the delete devices message to the edge asynchronously.

Downstream
- Request TOPIC: `/ext/session/{productKey}/{deviceKey}/combine/delete`

- Reply TOPIC: `/ext/session/{productKey}/{deviceKey}/combine/delete_reply`

**Note:** The *productKey* and *deviceKey* in the TOPIC are the credentials of the edge.

## Example Request Message

```
{
	"id": "123",
	"version": "1.0",
	"params": [
            {
		"productKey": "xxx",
		"deviceKey": "xxx"
	}
	],
	"method": "combine.delete"
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
    <th>​Type​</th>
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
    <td>Object</td>
    <td>Mandatory </td>
    <td>Parameters used for deleting a sub-device.</td>
  </tr>
  <tr>
    <td>productKey</td>
    <td>String</td>
    <td>Mandatory</td>
    <td>Product Key of the sub-device.</td>
  </tr>
  <tr>
    <td>deviceKey</td>
    <td>String </td>
    <td>Mandatory</td>
    <td>Device key of the sub-device.</td>
  </tr>
  <tr>
    <td>method</td>
    <td>String</td>
    <td>Mandatory</td>
    <td>The method of the request. </td>
  </tr>
  <tr>
    <td>code</td>
    <td>String</td>
    <td>Mandatory </td>
    <td>Response code &ldquo;200&rdquo; or the error code defined on the device end. &ldquo;200&rdquo; indicates that the request operation is executed successfully. </td>
  </tr>
  <tr>
    <td>data</td>
    <td>JSON</td>
    <td>Optional </td>
    <td>Detailed returned information in JSON format. </td>
  </tr>
</table>
