# Batch Upgrading Device Firmware

For the firmware that has been verified, you may create a batch upgrade task, specify the upgrade strategy and methods, and start to push the upgrade messages. This topic describes how to create a batch upgrade task.

## About This Task

You cannot upgrade any device firmware that is already in a upgrade process.

The following configurations should be provided for a batch upgrade task:

### Strategy

The firmware upgrade OTA service of EnOS supports both snapshot and incremental upgrade policies.

- **Snapshot**: Devices that have reported firmware and falls into the upgrade version range form an closed list. Only the devices on this list will be upgraded and any newly-added devices will not be pushed new firmware even if they meet the upgrade requirements.

- **Increment**: Devices that have reported firmware and falls into the upgrade version range form an open list. Any newly-added devices that meet the upgrade requirements fall into the upgrade scope, and the list of devices to be upgraded are changing dynamically.

### Methods

You may select the Cloud Forced Push or Upon Device Request method.

- **Cloud forced push**: EnOS maintains the list of devices to be upgraded according to the upgrade policy, and pushes the upgrade requests to devices as per the upgrade sequence. If the devices are online, they will receive the upgrade request and start upgrading; if the devices are offline, they will receive the upgrade request after reconnection.

- **Upon device request**: EnOS maintains the list of devices to be upgraded, and judge whether a device falls in the scope of upgrade when the device sends an upgrade request. If yes, an available firmware version will be pushed to the device. The upgrade process will start after the device confirms to upgrade to this version.

### Schedule

For cloud forced push, you can select different schedules, or time ranges. The upgrade is allowed only within the selected schedule, and no upgrade request will be pushed outside the schedule. The minimum schedule allowed by EnOS is 30 minutes.


## Before You Start

- Complete [Verifying Firmware] (verifying_firmware).

## Procedure

1. Select **Device Management > OTA**;

2. Select the firmware to be upgraded, and then select **Batch Upgrade**;

3. In the popup window, enter the following parameters:

   .. csv-table::
      :widths: auto

      "Fields", "Definition"
      "Firmware Version", "You may select one or more version numbers to be upgraded"
      "Strategy", "You may select **Snapshot** or **Increment**. For more information about upgrade policies, see [Terminology](ota_concept)。"
      "Scope", "If you need to upgrade all the devices of the selected version, select **All devices**; if you want to upgrade some devices of this version, select **Target devices**."
      "Filter, ""
      "", "Available when **Target devices** is selected; you may filter the devices to be upgraded by DeviceKey, tag, attribute and asset tree."
      "DeviceKey", "Available when **Specify device key** is selected as the filter; you may enter the device key to filter devices."
      "Device tag", "Available when **Specify device tag value** is selected as the filter; you may filter devices by tag and tag value."
      "Device attribute", "Available when **Specify device attribute value** is selected as the filter; you may filter devices by attribute name and value."
      "Asset tree", "Available when **Specify asset tree** is selected as the filter; you may select devices based on the root nodes within the OU and the parent nodes under the root nodes; if the root nodes or parent nodes themselves are also devices, they will be taken into the upgrade scope; if you want to specify the devices of underlying child nodes, it should be achieved using DeviceKey. At most 5 asset trees may be selected."
      "Upgrade method", "Includes Cloud Forced Push and Upon Device Request; If you select to filter devices by specifying DeviceKey, tags, attributes or asset trees for directed upgrade, only "Cloud Forced Push" is available."
      "Schedule", "24 hours by default. EnOS Cloud only pushes upgrade request within the schedule."

4. Select **Confirm** to start the batch upgrade process;

## Results

In the process of **OTA Upgrade**, select **Upgrade Details** at the firmware to enter the upgrade details page; then, click **Upgraded successfully ** **Upgrade failed** tab page to view the results of batch upgrade. See [Viewing Upgrade Details](viewing_upgrade_detail)

## Subsequent operations

You may delete any necessary firmware after upgrading. See [Deleting Firmware](deleting_firmware)。
