# Asset Tree

Asset tree is a key function of EnOS Device Management service. Asset tree mainly targets to asset owners who understand the enterprise asset management business. Therefore, they can quickly create the asset topology to manage assets in the cloud.

The asset tree function and the device management function are decoupled, which means that the device management operation is independent of the asset management. Therefore, you can complete device management and connection first and then bind the connected devices to the nodes of the asset tree. You can also create an asset tree before you provision and connect the devices. Generally, a connected device is usually bound to a node of the asset tree.

## Key Concepts

### Asset Tree

An asset tree is the hierarchical organization of assets. An asset can be added to multiple asset trees so that the assets can be managed from different dimensions for different business scenarios. Scenarios for multiple asset trees are as follows:

- Management based on geographical location: country, state, city, district, etc.
- Management based on industry domain: wind power, photovoltaic, energy storage, etc.
- Management based on device type: fan, inverter, combiner box, etc.

For the aforementioned scenarios, you can create three asset trees for the same group of assets.

### Node

An asset node is the minimum element that forms an asset tree. A node can be associated with one asset or left blank without binding to any asset.
Each node of an asset tree has a unique identifier. An asset can be bound to different asset trees and to different nodes of the same asset tree.

The relationship between asset trees, nodes, assets, and devices is shown in the following figure:

.. image:: ../media/asset_tree.png
   :alt: Fig. Asset Trees Overview


- Asset 1 is bound to Tree 1 and Tree 2.
- Node 5 of Tree 2 is left blank to allow a later binding of asset.
- Asset 3 is a device and is a child of Asset 2.

## Related Information

- [Getting Started with Asset Tree](gettingstarted_assettree)
