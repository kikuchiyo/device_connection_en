# Managing Devices

This topic describes the device management operations such as how to view and change device status, how to obtain device secret credentials, and more.

## Before You Start

- To manage devices, you must have write access to the **Connectivity Management** service. If you don't have the access, contact your OU administrator to obtain the access. For more information about user access in EnOS, see [Policy, Roles, and Access](/docs/iam/en/dev/access_policy).

- To learn about the activation and running status of a device, see [Secret-based One-way Authentication](../../../learn/deviceconnection_authentication).

## Viewing Device Status

1. In the EnOS Console, select **Device Management > Device**.

2. In the table of devices, you can view the device status in the **Status/Enable** column.

The "Inactive" status is displayed only when the product is not activated. Once the product is activated, the running status - online or offline - will be displayed in the table.

## Device Online/Offline

When a device is in operation, you can change its status by turning it on or off.

If the device is found to be abnormal, it can be disabled in EnOS.

1. In the EnOS Console, select **Device Management > Device**.

2. In the table of devices, you can specify a device as online or offline by the switch in the **Status/Enable** column.

## Retrieving the Device Triple Information

The `productKey`, `deviceKey`, and `deviceSecret` are considered as the device triple information.

1. In the EnOS Console, select **Device Management > Device**.

2. In the table of devices, for the target device, click **View** to open the **Device Details** page.

3. Find the `productKey`, `deviceKey`, and `deviceSecret` of the device.
