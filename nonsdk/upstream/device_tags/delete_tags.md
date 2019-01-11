# Delete Tags

Upstream
- Request TOPIC `/sys/{productKey}/{deviceName}/thing/tag/delete`

- Reply TOPIC `/sys/{productKey}/{deviceName}/thing/tag/delete_reply`

## Example Request Message

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

## Example Response Message

```
{
 "id": "123",
 "code": 200,
 "data": {}
}

```

## Parameter Description

.. list-table::
   :widths: 20 20 20 40

   * - Parameter</td>
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
      When not specified, no tag is deleted. </td>
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
    <td>Response code. &ldquo;200&rdquo; indicates that the requested operation is executed successfully.</td>
  </tr>
  <tr>
    <td>data</td>
    <td>JSON</td>
    <td>Optional</td>
    <td>Detailed returned information in JSON format.</td>
  </tr>
</table>
<!--end-->
