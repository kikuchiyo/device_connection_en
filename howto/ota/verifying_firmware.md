# Verifying Firmware

After adding a new firmware and batch upgrading the firmware, you should select one or more versions to be upgraded, specify a small batch of devices for firmware upgrade, and verify whether the firmware can be pushed to the device end and whether the firmware can be upgraded normally to avoid any loss due to batch upgrading wrong firmware.

.. note:: EnOS only provides the message channels for upgrade verification, so the developers need verify whether the firmware can be pushed to the device and whether the device with firmware updated can run normally.

## Task description

This article describes how to batch verify the device firmware. The batch upgrade is not allowed for any unverified device firmware. New upgrade task is impossible for any firmware under firmware upgrade status.

## Prerequisites

- Completed the step [Adding Firmware](adding_firmware)
- The device has escalated its firmware version and `deviceKey`

## Steps

1. Select **Device Management > OTA Upgrade**;

2. Identify the device to be verified, select **Verify Firmware**, select the version number to be upgraded and the deviceKey of the device that meets the version number requirements; if any verification has been performed previously, the results of the last verification will pop up; at this point, click **Re-verify**, and a window will pop up for you to enter the version number to be upgraded and the deviceKey;

   .. csv-table::
      :widths: auto

      "Fields", "Comments"
      "Version numbers to be upgraded", "A list of the version numbers escalated by the devices; if no version information is escalated by the devices, the message **No version number is escalated by the devices**"
      "Device's DeviceKey", "deviceKey of the devices that comply with the version numbers selected by the user; at most 5 devices are allowed to be selected for verifying firmware each time"

3. Click **Verify** to start the device firmware verification. The meanings of each item in the list of device firmware upgrade statuses are given as follows; 

   .. csv-table::
      :widths: auto

      "Fields", "Meanings"
      "deviceKey", "deviceKey of the device subject to firmware verification"
      "Upgrade status", "The device that has not received the cloud forced push is set as **To be upgraded**; the device for which the upgrade has been escalated is set as  **In progress**; the device for which the upgraded has been completed is set as **Upgraded successfully** or **Upgrade failed**"
      "Cancel upgrade", "For the devices under the  **To be upgraded** status, you may click **Cancel Upgrade** to cancel the firmware upgrade task. For the devices under other statuses, **Cancel Upgrade** is disabled."

## Results

Either the result **Upgraded successfully** or **Upgrade failed** will occur for the devices subject to firmware verification. No matter which result occurs, the status of firmware will always change to **Verified**. You may select **Re-verify**, and then select the version numbers to be upgraded and deviceKey for re-verification purpose, or select **OK** to finish the verification process.

.. note:: In case that there is any device subject to the **To be upgraded** status, the firmware upgrade task to be performed for this device will be canceled if you select **Re-verify**; in the popping firmware verification window, you can select the same firmware version again, and re-select the device for which the task is just canceled and the devices with a result of **Upgraded failed** to re-verify their firmware.

.. note:: After upgrading the device firmware, the developer should verify whether the device functions well or not, depending on specific conditions of the device.

## Subsequent operations

[Batch Upgrading Firmware](batch_upgrading_firmware)
