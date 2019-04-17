# Batch Upgrading Firmware

For a verified firmware, you can create a batch upgrade task, specify the upgrade strategy and methods, and start to push the upgrade requests. This topic describes how to batch upgrade firmwares.

## About This Task

You cannot upgrade any device firmware that is already in an upgrade process.

The following configurations should be provided for a batch upgrade task:

### Strategy

EnOS supports both snapshot and incremental upgrade strategies.

- **Snapshot**: Devices that have reported firmware version and fall into the upgrade list form a closed list. Only the devices on this list will be upgraded and any devices added later will not receive new firmware push even if they meet the upgrade requirements.

- **Increment**: Devices that have reported firmware and falls into the upgrade list form an open list. Any devices added later that meet the upgrade requirements are included into the open list. The list of devices to be upgraded changes dynamically.

### Methods

You can select cloud forced push or upon device request.

- **Cloud forced push**: EnOS maintains the list of devices to be upgraded according to the upgrade policy, and pushes the upgrade requests to devices as per the upgrade sequence. If the devices are online, they will receive the upgrade request and start upgrading; if the devices are offline, they will receive the upgrade request after reconnection.

- **Upon device request**: EnOS maintains the list of devices to be upgraded, and judge whether a device falls in the scope of upgrade when the device sends an upgrade request. If yes, an available firmware version will be pushed to the device. The upgrade process will start after the device confirms to upgrade to this version.

### Schedule

For cloud forced push, you can select different schedules, or time ranges. The upgrade is allowed only within the selected schedule, and no upgrade request will be pushed outside the schedule. The minimum schedule interval allowed by EnOS is 30 minutes.


## Before You Start

- Completed [Verifying Firmware](verifying_firmware).

## Procedure

1. Select **Device Management > OTA**;

2. For the firmware to be upgraded, and then select **Batch Upgrade**;

3. In the pop-up window, enter the following parameters:

   .. csv-table::
      :widths: auto

      "Fields", "Definition"
      "Firmware Version", "You can select one or more version numbers to be upgraded"
      "Strategy", "You can select **Snapshot** or **Increment**."
      "Scope", "If you need to upgrade all the devices of the selected version, select **All devices**; if you want to upgrade some devices of this version, select **Target devices**."
      "Filter, "Available when **Target devices** is selected; you can filter the devices to be upgraded by DeviceKey, tag, attribute and asset tree."
      "DeviceKey", "Available when **Specify device key** is selected as the filter; you can enter the device key to filter devices."
      "Tag", "Available when **Specify device tag value** is selected as the filter; you can filter devices by tag and tag value."
      "Attribute", "Available when **Specify device attribute value** is selected as the filter; you can filter devices by attribute name and value."
      "Asset tree", "Available when **Specify asset tree** is selected as the filter; you can select devices based on the root nodes of the OU and the parent nodes under the root nodes; if the root nodes or parent nodes themselves are also devices, they will fall into the upgrade scope; if you want to specify the devices on the underlying child nodes, specify by their deviceKey. A maximum of 5 asset trees can be selected."
      "Upgrade method", "Includes cloud forced push and upon device request; If you filter devices by DeviceKey, tags, attributes or asset trees for specific devices, only "Cloud Forced Push" is available."
      "Schedule", "24 hours by default. EnOS Cloud only pushes upgrade request within the schedule."

4. Select **Confirm** to start the batch upgrade process;

## Result

In **OTA**, select **Details** to enter the upgrade details page; then, click **Upgraded successfully** **Upgrade failed** tab page to view the results of batch upgrade. See [Viewing Upgrade Details](viewing_upgrade_detail)

## Next Step

You can delete firmware after an upgrade. See [Deleting Firmware](deleting_firmware).
