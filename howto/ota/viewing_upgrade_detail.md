# Viewing Upgrade Details

The users can view the firmware upgrade status through upgrade details, and verify, batch upgrade, edit, and delete the firmware as needed.

## About This Task

This article describes how to view upgrade details and perform related operations.

## Before You Start

- Completed [Adding Firmware](adding_firmware)

## Procedure

1. Select **Device Management > OTA**

2. Select **Detail** for the firmware you want to view

   .. csv-table::
      :widths: auto

      "Tab Page","Description"
      "To be upgraded","Devices to be upgraded; you may select **Cancel Upgrade** for such devices"
      "In progress","The firmware upgrade starts and the upgrade progress is reported to EnOS; at this point, you can't cancel the upgrade"
      "Success","Refer to the devices whose firmware is upgraded successfully"
      "Failure","Refer to the device that fail to be upgraded with the failure reason described; you may select **Re-upgrade**"

## Result

The following list include common upgrade failure reasons that are listed in the Failure tab page.

- Upgrade failure
- Download failure
- Verification failure
- Burning failure

For more information, see [Developing OTA Capabilities on Devices](developing_device_ota). The device developers should troubleshoot errors according to the specific reason.

.. note:: If you select batch upgrade when a batch upgrade task already exists, you can only modify the schedule for batch upgrade task but are not allowed to add or delete firmware versions to be upgraded.

## Next Steps

You can perform [Verifying Firmware](verifying_firmware) again and perform [Batch Upgrading Firmware](batch_upgrade_firmware); for firmware that is no longer needed, you can perform [Deleting Firmware](deleting_firmware)
