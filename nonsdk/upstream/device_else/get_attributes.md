# Get Attributes

A device can publish a message to this topic to request EnOS cloud to retrieve the attributes from the cloud.

**Note:** Configure the parameters according to the output and input parameters of the measuring points.

Upstream
- Request TOPIC: /sys/{productKey}/{deviceKey}/thing/attribute/query

- Reply TOPIC: /sys/{productKey}/{deviceKey}/thing/attribute/query_reply

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
    <td>Version of the protocol. Current version is   1.0.</td>
  </tr>
  <tr>
    <td>params</td>
    <td>List</td>
    <td>Mandatory</td>
    <td>Parameters used for deleting tags.</td>
  </tr>
  <tr>
    <td>attributes </td>
    <td>Array </td>
    <td>Mandatory</td>
    <td>List of the  attribute. One request can contain maximum 200   items.<br>
       If the value of attributes is null, system  will retrieve all the attributes.  </td>
  </tr>
  <tr>
    <td>method</td>
    <td>String</td>
    <td>Mandatory</td>
    <td>The method of the request.</td>
  </tr>
  <tr>
    <td>attr1</td>
    <td>String </td>
    <td>Mandatory</td>
    <td>The unique  identifier of the attribute. </td>
  </tr>
  <tr>
    <td>value</td>
    <td>String</td>
    <td>Mandatory</td>
    <td><br>
      The value of the tags. </td>
  </tr>
  <tr>
    <td>code</td>
    <td>Integer</td>
    <td>Mandatory</td>
    <td>Response code. &ldquo;200&rdquo; indicates the request is   executed successfully.</td>
  </tr>
</table>
