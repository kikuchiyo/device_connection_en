# Device Registration

## Register a sub-device

- Request TOPIC: /sys/{productKey}/{deviceKey}/thing/device/register

- Reply TOPIC: /sys/{productKey}/{deivceKey}/thing/device/register_reply

### Example request message

```
{

"id": "123",

"version": "1.0",

"params": [

{

"productKey": "1234556554",

"deviceAttributes": {

"color":"red"

},

"deviceKey" : "deviceKey1234",

"deviceName": "deviceName1234",

"deviceDesc": "deviceDesc1234"

}

],

"method": "thing.device.register"

}
```

### Example response message

```
{

"id": "123",

"code": 200,

"data": [

{

"assetId": "12344",

"productKey": "1234556554",

"deviceKey": "deviceKey1234",

"deviceSecret": "xxxxxx"

}

]

}
```

### Parameter Description

<table>
  <tr>
    <td>Parameter</td>
    <td>Type</td>
    <td>Occurrence </td>
    <td>Description</td>
  </tr>
  <tr>
    <td>Id</td>
    <td>Long </td>
    <td>Mandatory</td>
    <td>Message ID. Reserved parameter for future   use. </td>
  </tr>
  <tr>
    <td>Version </td>
    <td>String </td>
    <td>Mandatory </td>
    <td>Version of the protocol. Current version is   1.0. </td>
  </tr>
  <tr>
    <td>Params </td>
    <td>List </td>
    <td>Mandatory </td>
    <td>Parameters used for dynamic registration. </td>
  </tr>
  <tr>
    <td>deviceAttributes </td>
    <td>String </td>
    <td>Optional </td>
    <td>List of the attributes of the device. </td>
  </tr>
  <tr>
    <td>Color </td>
    <td>String </td>
    <td>Optional </td>
    <td>Attribute of the device </td>
  </tr>
  <tr>
    <td>deviceKey </td>
    <td>String </td>
    <td>Optional </td>
    <td>DeviceKey of the sub-device. </td>
  </tr>
  <tr>
    <td>deviceName </td>
    <td>String </td>
    <td>Optional </td>
    <td>Name of the sub-device. </td>
  </tr>
  <tr>
    <td>deviceDesc</td>
    <td>String</td>
    <td>Optional</td>
    <td>Description of the sub-device.</td>
  </tr>
  <tr>
    <td>productKey</td>
    <td>String</td>
    <td>Mandatory</td>
    <td>Productkey of the sub-device.</td>
  </tr>
  <tr>
    <td>assetId </td>
    <td>String</td>
    <td>Mandatory</td>
    <td>Unique identifier of the sub-device. </td>
  </tr>
  <tr>
    <td>deviceSecret</td>
    <td>String </td>
    <td>Mandatory</td>
    <td>DeviceSecret of the sub-device</td>
  </tr>
  <tr>
    <td>Method</td>
    <td>String</td>
    <td>Mandatory</td>
    <td>The method of the request.</td>
  </tr>
  <tr>
    <td>Code</td>
    <td>Integer</td>
    <td>Mandatory</td>
    <td>Response code. &ldquo;200&rdquo; indicate the request   is executed successfully.</td>
  </tr>
  <tr>
    <td>Data</td>
    <td>String </td>
    <td>Optional</td>
    <td>Detailed information of the sub-device, in JSON format. </td>
  </tr>
</table>
