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
     "value2": 9
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
    <td>attribute </td>
    <td>Array</td>
    <td>Optional</td>
    <td>List of the attributes-type of features of the device. A request can carry a maximum of 200 attributes.<br>
       When not specified, no attribute will be reported.  </td>
  </tr>
  <tr>
    <td>method</td>
    <td>String</td>
    <td>Mandatory</td>
    <td>The method of the request.</td>
  </tr>
  <tr>
    <td>attr1</td>
    <td>Struct</td>
    <td>Mandatory</td>
    <td>The identifier of the attribute that you want to report, in this example, the attribute with the identifier of <strong>attr1</strong>. The format here must match the data type defined for this parameter. For example, when the data type of this parameter is struct. the data here must be match the defined struct which is <strong>value</strong> and <strong>value2</strong>. </td>
  </tr>
  <tr>
    <td>value</td>
    <td>Integer</td>
    <td>Mandatory</td>
    <td>The parameter name of the struct data of this attribute, in this example, the parameter named <strong>value</strong>. The value you set must match the data type defined for this parameter. For example, when the data type of this parameter is set to integer in the thing model, the value here must be an integer. </td>
  </tr>
  <tr>
    <td>code</td>
    <td>Integer</td>
    <td>Mandatory</td>
    <td>Response code. &ldquo;200&rdquo; indicates that the requested operation is executed successfully.</td>
  </tr>
</table>
