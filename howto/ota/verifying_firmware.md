# Verifying Firmware

After adding a new firmware, you should select one or multiple firmware versions and batch upgrade them to test whether new firmware versions can be pushed to devices and whether firmware can be upgraded. This is to avoid any loss caused by batch upgrading wrong firmware.

.. note:: EnOS provides only the message channels for verification. Developers need to verify whether the firmware can be pushed to the device and whether the upgraded device can operates properly.

## About This Task

This topic describes how to batch verify device firmware. You can batch upgrade verified firmware only. You cannot start new upgrade task for a device if the device is already being upgraded.

## Before You Start

- Completed [Adding Firmware](adding_firmware)
- The device has reported its firmware version and `deviceKey` to EnOS.

## Procedure

1. Select **Device Management > OTA**;

2. Identify the firmware to be verified, select **Verify**. Select the version number to be upgraded and the deviceKeys of the device of the selected firmware version; if any verification has been performed previously, the results of the last verification will be displayed. Click **Re-verify**, and a window will pop up for you to enter the version number to be upgraded and the deviceKeys;

   .. csv-table::
      :widths: auto

      "Fields", "Description"
      "Version numbers to be upgraded", "A list of the version numbers reported by the devices; if no version information is reported by the devices, message **No version number is reported by the devices** is displayed."
      "DeviceKey", "deviceKey of the devices of the version numbers you selected; you can select at most 5 devices to verify each time"

3. Click **Verify** to start verification.  

   .. csv-table::
      :widths: auto

      "Fields", "Description"
      "deviceKey", "deviceKey of the device to be verified"
      "Upgrade status", "For devices that have not received a firmware push, the status is **To be upgraded**; for devices that are being upgraded, the status is **In progress**; for devices that have completed an upgrade, the status is **Upgraded successfully** or **Upgrade failure**"
      "Cancel upgrade", "For devices to be upgraded, you can click **Cancel Upgrade** to cancel the firmware upgrade task. For devices whose status is not **To be upgraded**, you cannot cancel the upgrade."

## Result

For devices you choose to verify, they may be upgraded successfully or fail to be upgraded. Whatever the result, the status of the firmware will become **Verified**. You can select **Re-verify**, and then select the version numbers to be upgraded and the deviceKeys for re-verification, or select **OK** to finish the verification.

.. note:: If there is any device to be upgraded, selecting **Re-verify** would cancel the existing firmware upgrade task. To restart the disrupted tasks, select the same firmware version again in the pop-up window after selecting **Re-verify**, and re-select the devices whose upgrade was just canceled. You can also include the devices that failed to be upgraded.

.. note:: After upgrading, the developer should verify whether the device functions properly.

## Next Steps

[Batch Upgrading Firmware](batch_upgrading_firmware)
