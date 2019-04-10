# Firmware OTA Upgrade Overview

EnOS provides the firmware OTA (Over-the-Air) upgrade service for devices. This service allows that the cloud pushes the messages for managing and upgrading the firmware versions to meet the bug fixing, capability upgrading and other requirements after devices are deployed.

## Full lifecycle management of firmware versions

You can use the EnOS Console to achieve the full lifecycle management of firmware versions, create new firmware versions and set upgrade policies. The cloud automatically pushes the upgrade requests for the selected devices, and records their upgrade progress and results.

The lifecycle management process of firmware versions in EnOS is described as follows:

.. image:: media/ota_lifecycle_management.png

## Device SDK for OTA

Provides the device SDK to encapsulate the message interfaces for version escalation and upgrading. The devices should implement by themselves the specific firmware switching logic and escalate the upgraded firmware versions.

## Firmware OTA upgrade process

EnOS supports the following firmware upgrade modes:

- **Upgrade pushed actively in cloud**: The cloud pushes the forced upgrade to the device end, where it is required to specify the version number to which the device is upgraded
- **Upgrade upon request from device end**: The device owners or O&M personnel decide whether to upgrade the firmware; the device sends an upgrade request only after it is decided to upgrade the firmware

### Upgrade pushed actively in cloud

This process is shown in the figure below:

.. image:: media/cloud_pushed_ota_process.png

After the batch upgrade task is created in cloud, the scope of the devices to be upgraded is maintained as per the upgrade policies and the cloud pushes the upgrade request to the devices as per the upgrade sequence:
- If the devices are online, the upgrade process will start once they receive the upgrade request
- If the devices are offline, they will receive the upgrade request when they connect to the cloud next time 

The upgrade pushed actively in cloud is forced upgrade request. Generally, the devices will start the upgrade process once they receive the request and escalate their new versions after rebooting. However, whether to perform the forced upgrade depends on the implementation on the device end, and the developer may add a local upgrade confirmation logic for the downloaded OTA firmware so that the new firmware booting area will be switched to only after local confirmation.

### Upgrade upon request from device end

This process is shown in the figure below:

.. image:: media/update_upon_request_ota.png

After creating the batch upgrade task in cloud, you may select the upgrade mode as **Upon device request**. At this point, the cloud will not push the upgrade request to the devices immediately but only maintain the list of devices to be upgraded. Only after the devices send the upgrade request actively and are qualified within the upgrade scope can the firmware version information for upgradeable devices be returned, and the upgrade process will start after the upgrade task is confirmed at the device end.

The upgrade upon request from device end is an optional upgrade mode, which adds manual intervention and confirmation steps. In some cases, you do not need to force the device to be upgraded but decide whether to upgrade the devices with reference to their actual conditions.

## Get started

1. Use SDK to develop the device end OTA capabilities, [Learn More](developing_device_ota)。
2. Add the device firmware in the cloud, [Learn More](adding_firmware)。
3. Upgrade the firmware for a small batch of devices and verify whether the firmware can be pushed to the device end normally and whether the firmware can be upgraded normally, [Learn More](verifying_firmware).
4. Configure the batch upgrade task to upgrade the qualified devices as per the defined upgrade policies and methods within the schedule, [Learn More](batch_upgrading_firmware).




