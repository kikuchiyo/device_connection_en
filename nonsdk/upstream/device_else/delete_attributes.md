# Delete Attributes

A device can publish a message to this topic to delete the attributes from the cloud.

Upstream
- Request TOPIC: `/sys/{productKey}/{deviceKey}/thing/attribute/delete`

- Reply TOPIC: `/sys/{productKey}/{deviceKey}/thing/attribute/delete_reply`

## Example Request Message

```
{
 "id": "123",
 "version": "1.0",
 "params": {
   "attributes": ["attr1", "attr2", "attr3"]
 },
 "method": "thing.attribute.delete"
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
    <th>Parameter</th>
    <th>Type</th>
    <th>Occurrence</th>
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
    <td>List</td>
    <td>Mandatory</td>
    <td>Parameters used for deleting attributes.</td>
  </tr>
  <tr>
    <td>attributes </td>
    <td>Array </td>
    <td>Optional</td>
    <td>List of the identifier of the attribute-type of features. A request can carry a maximum of 200 attributes.<br>
       When not specified, no attribute is deleted.</td>
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
</table>
