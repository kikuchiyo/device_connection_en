# Report Attributes

A device can publish a message to this topic to report the newly added attributes to the cloud.

Upstream
- Request TOPIC：`/sys/{productKey}/{deviceKey}/thing/attribute/update`

- Reply TOPIC：`/sys/{productKey}/{deviceKey}/thing/attribute/update_reply`

## Example Request Message

```
{
 "id": "123",
 "version": "1.0",
 "params": [
 "attributes": {
 "attr1": {
     "value": 1.0,
     "value2": "9"
   },
 "attr2": 1.02,
 "attr3": [1.02, 2.02, 7.93]
 }
 ],
 "method": "thing.attribute.update"
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
    <td>Parameters used for reporting attributes.</td>
  </tr>
  <tr>
    <td>attributes </td>
    <td>Array </td>
    <td>Optional</td>
    <td>List of the attributes. A request can carry a maximum of 200 attributes.<br>
       When not specified, all attributes are reported.  </td>
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
    <td>The unique identifier of the attribute. </td>
  </tr>
  <tr>
    <td>value</td>
    <td>String</td>
    <td>Mandatory</td>
    <td>The value of the tags. </td>
  </tr>
  <tr>
    <td>code</td>
    <td>Integer</td>
    <td>Mandatory</td>
    <td>Response code. &ldquo;200&rdquo; indicates that the requested operation is executed successfully.</td>
  </tr>
</table>
