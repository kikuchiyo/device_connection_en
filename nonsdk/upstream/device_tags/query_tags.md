# Query tags

Upstream
- Request TOPIC: /sys/{productKey}/{deviceKey}/thing/tag/query

- Reply TOPIC: /sys/{productKey}/{deviceKey}/thing/tag/query_reply

## Example Request Message

```
{
 "id": "123",
 "version": "1.0",
 "params": {
   "tags": ["tag1", "tag2"]
 },
 "method": "thing.tag.query"
}

```

## Example Response Message

```
{
 "id": "123",
 "code": 200,
 "data": {
   "tag1": "value1",
   "tag2": "value2"
 }
}

```

## Parameter Description

<body>
<table>
  <tr>
    <td>Parameter </td>
    <td>Type </td>
    <td>Description </td>
  </tr>
  <tr>
    <td>id</td>
    <td>Long</td>
    <td>Message ID. Reserved parameter for future use.</td>
  </tr>
  <tr>
    <td>version</td>
    <td>String</td>
    <td>Version of the protocol. Current version is   1.0.</td>
  </tr>
  <tr>
    <td>params</td>
    <td>Object</td>
    <td>Parameters used for quering sub-devics </td>
  </tr>
  <tr>
    <td>tags</td>
    <td>Object</td>
    <td>The unique identifier of the tags .<br>
      If the value of tags is null in the request topic, the request will query all the tags.</td>
  </tr>
  <tr>
    <td>method</td>
    <td>String</td>
    <td>The method of the request.</td>
  </tr>
  <tr>
    <td>code</td>
    <td>Integer</td>
    <td>Response   code. &ldquo;200&rdquo; indicates the request is executed successfully.</td>
  </tr>
</table>
