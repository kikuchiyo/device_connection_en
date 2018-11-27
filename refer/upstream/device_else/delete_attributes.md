# Delete attributes

- Request TOPIC: /sys/{productKey}/{deviceKey}/thing/attribute/delete

- Reply TOPIC: /sys/{productKey}/{deviceKey}/thing/attribute/delete_reply

## Example request message

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
    <td>Optional</td>
    <td>List of the unique   identifier of the attribute. One request can contain maximum 200 items.<br>
      The value of the attributes cannot be null. If the value is null,   no tags will be deteled.
      &nbsp;</td>
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
</table>
