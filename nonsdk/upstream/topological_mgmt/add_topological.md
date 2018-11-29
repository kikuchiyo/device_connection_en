# Add topological Relationships of sub-devices

An edge can publish a message to this topic to request EnOS Cloud to add
the topological relationship between the edge and a sub-device.

Upstream
- Request TOPIC: /sys/{productKey}/{deviceKey}/thing/topo/add

- Reply TOPIC: /sys/{productKey}/{deviceKey}/thing/topo/add_reply

**Note:** The *productKey* and *deviceKey* in the TOPIC are the parameters of the edge.

## Example Request Message

```
{
 "id": "123",
 "version": "1.0",
 "params": [
 {
 "deviceKey": "deviceKey1234",
 "productKey": "1234556554",
 "sign": "xxxxxx",
 "signmethod": "hmacSha1",
 "timestamp": "1524448722000",
 "clientId": "xxxxxx"
 }
 ],
 "method": "thing.topo.add"
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
    <td>Version of the protocol. Current version is 1.0.</td>
  </tr>
  <tr>
    <td>params</td>
    <td>List</td>
    <td>Mandatory</td>
    <td>Parameters used for adding topological relationships.</td>
  </tr>
  <tr>
    <td>deviceKey</td>
    <td>String</td>
    <td>Mandatory</td>
    <td>Device key of the sub-device.</td>
  </tr>
  <tr>
    <td>productKey</td>
    <td>String</td>
    <td>Mandatory</td>
    <td>Product key or the sub-device.</td>
  </tr>
  <tr>
    <td>sign</td>
    <td>String</td>
    <td>Mandatory</td>
    <td>Signature.</td>
  </tr>
  <tr>
    <td>signmethod</td>
    <td>String</td>
    <td>Mandatory</td>
    <td>Signing method. The supported methods are hmacSha1, hmacSha256, hmacMd5, and Sha256.</td>
  </tr>
  <tr>
    <td>timestamp</td>
    <td>String</td>
    <td>Mandatory</td>
    <td>Timestamp.</td>
  </tr>
  <tr>
    <td>clientId</td>
    <td>String</td>
    <td>Mandatory</td>
    <td>Identifier of the sub-device. The value can either be productKey or deviceKey.</td>
  </tr>
  <tr>
    <td>code</td>
    <td>Integer</td>
    <td>Mandatory</td>
    <td>Response code. &ldquo;200&rdquo; indicates the request is executed successfully.</td>
  </tr>
</table>

All parameters reported to EnOS Cloudwill be signed except **sign** and **signmethod**. The parameter names and values are sorted in alphabetical order and concatenated without concatenation symbols. The concatenated string is then signed by using the algorithm specified by **signmethod**. Taking the request message above for example, sign=uppercase(hmacsha1(deviceSecret, clientId123deviceKeytestproductKey123timestamp1524448722000)).
