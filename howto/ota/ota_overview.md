# Firmware OTA Upgrade Overview

You can upgrade device firmware by using the upgrade over-the-air (OTA) service. With this service, you can manage device firmware versions on EnOS and push new firmware versions to devices for bug fix and function upgrade.

## Full Lifecycle Management of Firmware Versions

You can use the EnOS Console to manage the full lifecycle of firmware versions, including creating new firmware versions and setting upgrade policies. EnOS automatically pushes the upgrade requests to the selected devices, and records their upgrade progress and results.

Lifecycle management in EnOS is as follows:

.. image:: media/ota_lifecycle_management.png

## Device SDK for OTA

Use the device SDK to encapsulate the messaging interfaces for version reporting and upgrading. Developers should ensure the new firmware can be activated on devices and reported to EnOS.

## Firmware OTA Upgrade Process

EnOS supports the following firmware upgrade modes:

- **Cloud forced push**: EnOS pushes the upgrade to the device, upgrading the device to a specified version
- **Upon device request**: The developer or O&M personnel sets policy deciding under what conditions a device should be upgraded. The devide sends an upgrade request to EnOS when it meets the conditions.

### Cloud Forced Push

This process is as follows:

.. image:: media/cloud_pushed_ota_process.png

After a batch upgrade task is created in EnOS, the list of devices to be upgraded is maintained as per the upgrade policy. EnOS pushes the upgrade request to the devices in order of the upgrade sequence:
- If the devices are online, the upgrade process will start once they receive the upgrade request
- If the devices are offline, they will receive the upgrade request when they connect to EnOS next time 

Cloud forced push is forced upgrade. Generally, the devices start the upgrade once they receive the request and report their new versions after rebooting. However, whether to perform the forced upgrade depends on the device settings. Device developers can still add a upgrade confirmation for the downloaded OTA firmware locally so that the partition storing the new firmware is activated only after confirmation.

### Upon Device Request

This process is as follows:

.. image:: media/update_upon_request_ota.png

After creating a batch upgrade task in EnOS, EnOS does not push the upgrade request to the devices immediately but maintains the list of devices to be upgraded. When devices send the upgrade requests to EnOS, EnOS decides whether the devices fall into the upgrade list. If the device can be upgraded, EnOS sends firmware versions that the device can be upgraded to to devices. The upgrade starts after the device confirms the upgrade.

Upgrade upon device request is an optional, which adds manual intervention and confirmation steps. In some cases, you do not need to force the device to be upgraded but decide whether to upgrade the devices as necessary.

## Get started

1. To use SDK to develop OTA capabilities on a device, see [Developing OTA Capabilities on Devices](developing_device_ota).
2. To add a device firmware in EnOS, see [Adding Firmware](adding_firmware).
3. To upgrade the firmware of a small batch of devices and verify whether the firmware can be pushed to the devices and whether the firmware can be upgraded, see [Verifying Firmware](verifying_firmware).
4. To configure a batch upgrade task to upgrade qualified devices as per the upgrade policy and methods within the schedule, see [Batch Upgrading Firmware](batch_upgrading_firmware).




