# Delete tags

Upstream
- Request TOPIC /sys/{productKey}/{deviceName}/thing/tag/delete

- Reply TOPIC /sys/{productKey}/{deviceName}/thing/tag/delete_reply

## Example request message

```
{
 "id": "123",
 "version": "1.0",
 "params": {
    "tags": ["tag1", "tag2"]
 },
 "method": "thing.tag.delete"
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
    <td>Parameter</td>
    <td>Type</td>
    <td>Occurrence</td>
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
    <td>Version of the protocol. Current version is 1.0.</td>
  </tr>
  <tr>
    <td>params</td>
    <td>List</td>
    <td>Mandatory</td>
    <td>Parameters used for deleting tags.</td>
  </tr>
  <tr>
    <td>tags</td>
    <td>List</td>
    <td>Mandatory </td>
    <td>The unique identifier of the tags.<br>
      The value of the tags cannot be null. If the value is null, no tag will be deleted. </td>
  </tr>
  <tr>
    <td>method</td>
    <td>String</td>
    <td>Mandatory</td>
    <td>The method of the request.</td>
  </tr>
  <tr>
    <td>code</td>
    <td>Integer</td>
    <td>Mandatory</td>
    <td>Response code. &ldquo;200&rdquo; indicates the request is   executed successfully.</td>
  </tr>
  <tr>
    <td>data</td>
    <td>String</td>
    <td>Optional</td>
    <td>Detailed information of the sub-device, in JSON   format.</td>
  </tr>
</table>
