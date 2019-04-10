# Adding Firmware

To upgrade firmware by using OTA in EnOS, you should add the device firmware on EnOS.

## About This Task

This topic describes how to add the firmware on EnOS. This step is the prerequisite to lifecycle management of device firmware on EnOS.

## Before You Start

- Make sure that the firmware to be managed is installed on the device and the device supports OTA upgrade.

## Procedure

1. Log into the EnOS Console, and select **Device Management > OTA**;

2. Select **Add Firmware** and provide the following information:

   - Products: You can select products created in **Device Management > Product** from the drop-down list;
   - Firmware Name: Supports Chinese characters, English letters and underlines, 4-32 characters, and no repetitive firmware names are allowed under the one product;
   - Firmware Version: No pre-defined format. No repetitive firmware version numbers are allowed under one product;
   - Signature Algorithm: Only MD5 signature is supported;
   - Select Firmware: click **Select File**, browse and upload local firmware. Supports `.bin`, `.tar`, `.gz` and `.zip`. The size of firmware should not exceed 100MB.
   - Version Description: no more than 100 characters. Devices can retrieve firmware description through the upgrade interface.

   <!--
   .. image:: media/ota_add_firmware.png
   -->
   .. note:: Once any wrong firmware is uploaded, you should delete the current firmware before adding the correct firmware.

3. Select **Confirm** to complete adding firmware.

## Example

As shown in the figure, we created a firmware named as "Sample Firmware":
<!--
.. image:: media/ota_added_firmware.png
-->
## Result

You may select **Add Firmware > OTA** to view the added firmware.

## Next Step

[Verifying Firmware](verifying_firmware)
