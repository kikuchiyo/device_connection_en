# Upgrading Firmware Over the Air

## About the scenario

Connecting remote devices to EnOS Cloud and managing its lifecycle end-to-end.

## Prerequisite

The device to be managed by EnOS Cloud must have OTA capacity, so that hardware developers can configure it with device SDK provided with EnOS.


## About This Task

After configuring the device, complete the following steps:
1. Add a firmware
2. Verify the firmware
3. Batch upgrade
4. View upgrade status

## Step 1：Add a Firmware

1. In the EnOS Console, select **Device Management > OTA**.
2. Select **Add firmware**, fill in the required information and click **Confirm**.


## Step 2：Verify the Firmware

For security, you must verify a firmware before upgrading it. Before batch upgrade, select one or multiple devices for verifying the firmware stability after upgrade

Select **Verify** on the firmware that you want to upgrade, enter the firmware version and device key, and click **Verify**.

The status of the firmware becomes verified after verification. You can then batch upgrade devices no matter the verification succeeded or not.


## Step 3：Batch Upgrade Devices

You can upgrade firmware for devices that have been verified.

1. Select **Batch Upgrade** and enter the required information in the pop-up window.


      **Scope**：If you want to upgrade all devices, select **All devices**; if you want to upgrade specific devices, select **Target devices** and filter the result based on DeviceKey, tag, attribute, and asset tree.

2. Select **Confirm**。


## Step 4: View Upgrade Status
Select **Upgrade Status** to check the upgrade result.
