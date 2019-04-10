# View Upgrade Details

The users can understand the firmware upgrade status by viewing upgrade details, and verify, batch upgrade, edit and delete the firmware as needed.

## Task description

This article describes how to view upgrade details and perform related operations.

## Prerequisites

- Completed the step [adding firmware](adding_firmware)

## Operation steps

1. Select **Device Management > OTA Upgrade**

2. Select **Upgrade Details** for the firmware to be viewed

   .. csv-table::
      :widths: auto

      "Tab Page","Descriptions"
      "To be upgraded","Refer to the selected devices to be upgraded; you may select **Cancel Upgrade** for such devices"
      "In progress","The device starts its firmware upgrade and the upgrade progress is escalated; at this point, you can't cancel upgrade"
      "Upgraded successfully","Refer to the devices for which the firmware is upgraded successfully"
      "Upgrade failed","Refer to the device that fail to be upgraded with briefed failure reason described; you may select **Re-upgrade**"

   
      

## Results

The common upgrade failure reasons are listed in the upgrade failure tab page.

- Upgrade failure
- Download failure
- Verification failure
- Burning failure

For more information, see [Developing Device End OTA](developing_device_ota). The device end developers should troubleshoot errors with reference to reasons.

.. note:: If you select batch upgrade when a batch upgrade task already exists, it is only possible to modify the schedule for batch upgrade task and it is not allowed to increase or delete the version number to be upgraded.

## Subsequent operations

You may perform [Verifying Firmware](verifying_firmware) again and perform [Batch Upgrade Firmware] (batch_upgrade_firmware); for any unnecessary firmware, you may perform [Deleting Firmware](deleting_firmware)
