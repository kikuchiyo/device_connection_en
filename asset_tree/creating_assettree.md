# Creating an Asset Tree

This article describes how to create an asset tree and attach the asset to the node of the asset tree.

## Creating a Root Node

To create a new asset tree, you should start from creating the root node of the asset tree. The name of the root node is used as the name of the asset tree.

1. In the EnOS Console, click **Asset Management** from the left side navigation panel.
2. Click  **+**  on the upper left corner to create the root node of the asset tree.
3. In the **Create Root Node** window, provide the following settings:
   - **Name**: Enter the asset tree name.
   - **Device Model**: Select an associated device model from the drop-down list.
       You can select a model for the root node of the asset tree. If the node does not need a model, you can use the built-in model `<None>`, which has four empty elements, for root node.
   - **Is Connected Device**: Choose `Yes` or `No` to indicate whether this device is a connected device or not.
        + The root node of the asset tree is generally not a connected device.

   - If you selected a model, provide corresponding values ​​according to the specifications defined in the thing model.

4. Click **Confirm** to complete creation.

## Adding a Leaf Node

After creating the root node, you can add a leaf node under the root node by the following approaches:
- Create an asset based on the model
- Add an existing asset to the asset tree


### Creating an Asset Based on the Model

1. Select a node of the asset tree and right click, then click **Add > Add leaf node > Create asset from model**.

2. Enter the asset name, select the device model from the drop down list, and specify whether the device to bind is a connected device or not. If `Yes`, you can bind this asset by the following approaches:

    - **Bind connected device**: Use this option if you have already created the device in the **Device Provisioning > Devices**. In this case, you'll bind the device to a node of the asset tree.
    - **Create connected device now**: Use this option if you haven't created the device in the **Device Provisioning > Devices** yet. In this case, you'll create a device and bind this device to a node of the asset tree. For how to create a new device, see [Creating a Device](../cloud/creating_device)
    - **Bind device later**: User this option if you are sure that the asset to be created is a connected device, but you need to confirm whether the device is created or not afterwards. In this case, you'll bind the device later.

3. Complete the configuration of the selected approach, and then click **Confirm**.


### Adding an Existing Asset

1. Select a node of the asset tree and right click, then click **Add > Add leaf node > Add existing node**.
2. Select the model for the asset and select the asset based on the model. Then click **Confirm** to complete the creation.

## Related Information

- [Asset Tree Overview](assettree_overview)
- [Managing an Asset Tree](managing_assettree)
