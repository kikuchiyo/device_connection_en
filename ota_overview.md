# EnOS Firmware Upgrade
Upgrade device firmware over-the-air (OTA) to maintain firmware, fix defects, and upgrade functions.

## Major Functionalities
**Device SDK**

Provides an SDK with OTA capacity for devices to report firmware version, request an upgrade, and report upgrade status.

**Firmware management**

Manages the lifecycle of devices, such as managing device information and creating, upgrading, verifying, and deleting firmware.

**Firmware log**

Logs the firmware upgrade process from end to end to trace firmware version and debug failed upgrades.

**Upgrade statistics**

Records statistics on firmware upgrade.

## Concepts

**OTA firmware upgrade**

Upgrading firmware over the air.

**Upgrade policy**

Maintenance of the device list that meets the upgrade requirements.

- **Snapshot**

    Upgrading only the devices on a closed list that meets the upgrade requirements.

- **Increment**
  
    Upgrading all the devices on an open list that meets the upgrade requirements where devices later added to the list will also be upgraded.

**Upgrade methods**

The procedure along which the devices on the list are upgraded

- **Cloud forced push**


    EnOS Cloud maintains the device list based on upgrade policy, pushing upgrade requests to devices. If the device is connected to EnOS Cloud, it accepts the request and starts upgrading; otherwise it accepts the request the next time it gets connected.
    

- **Upon device request**


   EnOS Cloud maintains the device list and determines whether a device firmware can be upgraded when the device requests upgrade. If the firmware is upgradable, EnOS Cloud pushes a new firmware version available to the device. The upgrade starts upon confirmation by the device.
