# Disconnect Sub-devices from EnOS Cloud

Upstream
- Request TOPIC: /ext/session/{productKey}/{deviceKey}/combine/logout

- Reply TOPIC: /ext/session/{productKey}/{deviceKey}/combine/logout_reply

## Example Request Message

```
{
 "id": 123,
 "params": {
 "productKey": "xxxxx",
 "deviceKey": "xxxxx"
 }
 "method":"combine.logout"
 "version":"1.0"
}

```

## Example Response Message

```
{
 "id": "123",
 "code": 200,
 "message": "",
 "data": {
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
    <td>id </td>
    <td>Long </td>
    <td>Optional </td>
    <td>Message ID. Reserved  parameter for future use. </td>
  </tr>
  <tr>
    <td>params </td>
    <td>List </td>
    <td>Mandatory </td>
    <td>Parameters used for disconnecting sub-devices from EnOS cloud </td>
  </tr>
  <tr>
    <td>deviceKey </td>
    <td>String </td>
    <td>Mandatory </td>
    <td>Device key of the sub-device. </td>
  </tr>
  <tr>
    <td>productKey </td>
    <td>String </td>
    <td>Mandatory </td>
    <td>Product key of a sub-device. </td>
  </tr>
  <tr>
    <td>code </td>
    <td>Integer </td>
    <td>Mandatory </td>
    <td>Response code. &ldquo;200&rdquo; indicates the request is executed  successfully. </td>
  </tr>
  <tr>
    <td>message </td>
    <td>String </td>
    <td>Optional </td>
    <td>Response message.</td>
  </tr>
  <tr>
    <td>data </td>
    <td>String </td>
    <td>Optional </td>
    <td>Additional information in the response, in JSON format. </td>
  </tr>
</table>
