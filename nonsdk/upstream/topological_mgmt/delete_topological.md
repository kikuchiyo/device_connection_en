# Delete Topological Relationships of Sub-devices

An edge can publish a message to this topic to delete the topological relationship between the edge and a sub-device.

After you delete the topological relationship of the sub-device, the sub-device can no longer connect to the EnOS Cloud through the edge.

Upstream
- Request TOPIC: `/sys/{productKey}/{deviceKey}/thing/topo/delete`

- Reply TOPIC: `/sys/{productKey}/{deviceKey}/thing/topo/delete_reply`

**Note:** The *productKey* and *deviceKey* in the TOPIC are the parameters of the edge.

## Example Request Message

```
"id": "123",
 "version": "1.0",
 "params": [
 {
 "deviceKey": "deviceKey1234",
 "productKey": "1234556554"
 }
 ],
 "method": "thing.topo.delete"
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
    <td>Parameters used for deleting topological relationships.</td>
  </tr>
  <tr>
    <td>deviceKey</td>
    <td>String</td>
    <td>Mandatory</td>
    <td>Device Key of the sub-device.</td>
  </tr>
  <tr>
    <td>productKey</td>
    <td>String</td>
    <td>Mandatory</td>
    <td>Product key of the sub-device.</td>
  </tr>
  <tr>
    <td>method</td>
    <td>String</td>
    <td>Mandatory</td>
    <td>Signing method. </td>
  </tr>

  <tr>
    <td>code</td>
    <td>Integer</td>
    <td>Mandatory</td>
    <td>Response code. &ldquo;200&rdquo; indicates that the requested operation is executed successfully.</td>
  </tr>
</table>
