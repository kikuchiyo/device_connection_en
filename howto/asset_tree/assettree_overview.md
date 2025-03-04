# Asset Tree Overview

Asset tree is a key function of EnOS Device Management service. Asset tree mainly targets to asset owners who understand the enterprise asset management business. Therefore, they can quickly create the asset topology to manage assets in the cloud.

The asset tree function and the device management function are decoupled, which means that the device management operation is independent of the asset management. Therefore, you can complete device management and connection first and then bind the connected devices to the nodes of the asset tree. You can also create an asset tree before you provision and connect the devices. Generally, a connected device is usually bound to a node of the asset tree.

## Key Concepts

### Asset Tree

An asset tree is the hierarchical organization of assets. An asset can be added to multiple asset trees so that the assets can be managed from different dimensions for different business scenarios. Scenarios for multiple asset trees are as follows:

- Management based on geographical location: country, state, city, district, etc.
- Management based on industry domain: wind power, photovoltaic, energy storage, etc.
- Management based on device type: fan, inverter, combiner box, etc.

For the scenarios above, you can create three asset trees for the same group of assets.

### Asset

An asset is the minimum element that forms an asset tree. It can be bound to a node on an asset tree.

Assets can be divided into device assets and logical assets. A device asset is a physical device, for example, a photovoltaic inverter, or a wind turbine. A logical asset can be a place to hold devices or a collection of devices, such as a site, an area, or a floor.

Each asset of an asset tree has a unique identifier. An asset can be bound to different asset trees and must be unique under one asset tree.

The relationship between asset trees, assets, and devices is shown in the following figure:


.. image:: ../../media/asset_tree.png
   :width: 300px

If a user deleted a device in **Device Management**, the corresponding asset bound to the asset tree node becomes an invalid node.

Except for an invalid node, you can continue to bind assets to every node on an asset tree. The maximum layers that an asset tree can have is 7, including the root layer. On each layer except the root layer, a maximum of 10000 peer assets are allowed to exist.

- Asset 1 is bound to Tree 1.
- Asset 3 is a device and is a child node of Asset 2.

## Related Information

- [Getting Started with Asset Tree](gettingstarted_assettree)
