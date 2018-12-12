# Get Attributes

A device can publish a message to this topic to retrieve attributes from the cloud.

Upstream
- Request TOPIC: `/sys/{productKey}/{deviceKey}/thing/attribute/query`

- Reply TOPIC: `/sys/{productKey}/{deviceKey}/thing/attribute/query_reply`

## Example Request Message

```
{
 "id": "123",
 "version": "1.0",
 "params": {
   "attributes": ["attr1", "attr2", "attr3"]
 },
 "method": "thing.attribute.query"
}

```

## Example Response Message

```
{
 "id": "123",
 "code": 200,
 "data": {
   "attr1": {
       "value": 1.0,
       "value2": "9"
     },
   "attr2": 1.02,
   "attr3": [1.02, 2.02, 7.93]
 }
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
    <td>Parameters used for getting attributes.</td>
  </tr>
  <tr>
    <td>attributes </td>
    <td>Array </td>
    <td>Mandatory</td>
    <td>List of the identifier of the attribute-type of features. A request can carry maximum 200 items.<br>
       When not specified, system will retrieve all the attributes.  </td>
  </tr>
  <tr>
    <td>attr1</td>
    <td>String </td>
    <td>Mandatory</td>
    <td>The unique identifier of the attribute. </td>
  </tr>
  <tr>
    <td>method</td>
    <td>String</td>
    <td>Mandatory</td>
    <td>The method of the request.</td>
  </tr>
  <tr>
    <td>value</td>
    <td>Struct</td>
    <td>Mandatory</td>
    <td>The detailed returned information of this attributes. In this example, the data type of this attribute is struct. Therefore, the parameter <strong>value</strong> is returned with its value. </td>
  </tr>
  <tr>
    <td>code</td>
    <td>Integer</td>
    <td>Mandatory</td>
    <td>Response code. &ldquo;200&rdquo; indicates that the request operation is executed successfully. </td>
  </tr>
</table>
