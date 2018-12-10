# Connect Sub-devices to EnOS Cloud

Upstream
- Request TOPIC: `/ext/session/{productKey}/{deviceKey}/combine/login`

- Reply TOPIC:    `/ext/session/{productKey}/{deviceKey}/combine/login_reply`

## Example Request Message

```
{
 "id": "123",
 "params": {
 "productKey": "123",
 "deviceKey": "test",
 "clientId": "123",
 "timestamp": "123",
 "signMethod": "hmacmd5",
 "sign": "xxxxxx",
 "cleanSession": "true"
 }
 "method":"combine.login"
}

```

## Example Response Message

```
{
 "id":"123",
 "code":200,
 "message":""
 "data": {
  }
}

```

All parameters reported to EnOS Cloudwill be signed
except **sign** and **signmethod**. The parameter names and values are
sorted in alphabetical order and concatenated without concatenation
symbols. The concatenated string is then signed by using the algorithm
specified by **signmethod**. Taking the request message above for
example, sign= uppercase(hmac_md5(deviceSecret,
cleanSessiontrueclientId123deviceKeytestproductKey123timestamp123)).

## Parameter Description

<table>
  <tr>
    <th>Parameter</th>
    <th>Type</th>
    <th>Occurrence</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>id </td>
    <td>Long </td>
    <td>Optional </td>
    <td>Message ID. Reserved parameter for future use. </td>
  </tr>
  <tr>
    <td>params </td>
    <td>List </td>
    <td>Mandatory </td>
    <td>Parameters used for connecting sub-device to EnOS Cloud. </td>
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
    <td>Product key of the sub-device </td>
  </tr>
  <tr>
    <td>sign</td>
    <td>String</td>
    <td>Mandatory</td>
    <td>Signature of the sub-device. Sub-devices use the same signature rules as the edge. </td>
  </tr>
  <tr>
    <td>signmethod </td>
    <td>String </td>
    <td>Mandatory </td>
    <td>Signing method. The supported methods are <em>hmacSha1</em>. </td>
  </tr>
  <tr>
    <td>timestamp </td>
    <td>String </td>
    <td>Mandatory </td>
    <td>Timestamp </td>
  </tr>
  <tr>
    <td>clientId </td>
    <td>String </td>
    <td>Mandatory </td>
    <td>Identifier of   the device client. The value can either be productKey or deviceName. </td>
  </tr>
  <tr>
    <td>cleanSession </td>
    <td>String </td>
    <td>Mandatory</td>
    <td>Supported   value: True. This   indicates to clear offline information for all sub-devices, which is   information that has not been received by QoS 1. </td>
  </tr>
  <tr>
    <td>message </td>
    <td>String</td>
    <td>Mandatory</td>
    <td>Response message </td>
  </tr>
  <tr>
    <td>data</td>
    <td>String </td>
    <td>Optional</td>
    <td>Detailed information of the sub-device, in JSON format. </td>
  </tr>
  <tr>
    <td>code</td>
    <td>Integer</td>
    <td>Mandatory</td>
    <td>Response code.   &ldquo;200&rdquo; indicates the request is executed successfully. </td>
  </tr>
</table>

**Note**: A edge can accommodate a maximum of 200 online sub-devices
simultaneously. When the maximum number is reached, the edge rejects any
connection requests.
