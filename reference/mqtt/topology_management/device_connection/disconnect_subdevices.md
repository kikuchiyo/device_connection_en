# Disconnect Sub-devices from EnOS Cloud

Upstream

- Request TOPIC: `/ext/session/{productKey}/{deviceKey}/combine/logout`

- Reply TOPIC: `/ext/session/{productKey}/{deviceKey}/combine/logout_reply`

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

.. list-table::
   :widths: 20 20 20 40

   * - Parameter
     - Type
     - Occurrence
     - Description
   * - id
     - Long
     - Optional
     - Message ID. Reserved parameter for future use.
   * - params
     - List
     - Mandatory
     - Parameters used for disconnecting sub-devices from EnOS cloud
   * - deviceKey
     - String
     - Mandatory
     - Device key of the sub-device.
   * - productKey
     - String
     - Mandatory
     - Product key of a sub-device.
   * - code
     - Integer
     - Mandatory
     - Response code. &ldquo;200&rdquo; indicates the request operation is executed successfully.
   * - message
     - String
     - Optional
     - Response message.
   * - data
     - JSON
     - Optional
     - Detailed returned information in JSON format.

<!--end-->
