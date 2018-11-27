# Get topological relationships of sub-devices

An edge can publish a message to this topic to request EnOS Cloud to retrieve the topological relationship between the edge and a sub-device.

- Request TOPIC: /sys/{productKey}/{deviceKey}/thing/topo/get

- Reply TOPIC: /sys/{productKey}/{deviceKey}/thing/topo/get_reply

**Note:** The *productKey* and *deviceKey* in the TOPIC are the parameters of the edge.

## Example Request Message

```
{

"id": "123",

"version": "1.0",

"params": {},

"method": "thing.topo.get"

}
```

## Example Response Message

```
{

"id": "123",

"code": 200,

"data": [

{

"deviceKey": "deviceKey1234",

"productKey": "1234556554"

}

]

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
    <td>Mandatory</td>
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
    <td>Object</td>
    <td>Optional</td>
    <td>Parameters used for getting topological   relationships.</td>
  </tr>
  <tr>
    <td>method</td>
    <td>String</td>
    <td>Mandatory</td>
    <td>The method of the request.</td>
  </tr>
  <tr>
    <td>deviceKey</td>
    <td>String</td>
    <td>Mandatory</td>
    <td>DeviceKey of the sub-device.</td>
  </tr>
  <tr>
    <td>productKey</td>
    <td>String</td>
    <td>Mandatory</td>
    <td>Product key of the sub-device.</td>
  </tr>
  <tr>
    <td>code</td>
    <td>Integer</td>
    <td>Mandatory</td>
    <td>Response code. &ldquo;200&rdquo; indicates the request is   executed successfully.</td>
  </tr>
  <tr>
    <td>data </td>
    <td>String </td>
    <td>Optional</td>
    <td>Detailed   information of the sub-device, in JSON format. </td>
  </tr>
</table>
