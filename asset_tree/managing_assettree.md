# Managing Asset Trees

This article describes the asset tree management operations from two aspects: asset and node.
- The operations of the node only affect the node.
- The operations of the asset affect all nodes that the asset is attached to.


## Deleting Asset Tree

Deleting an asset tree is accomplished by deleting the root node of the asset tree. You can delete a root node in the following approaches:
- Delete node
- Delete instance

  For a root node, we recommend using **Delete instance**, which will delete both the node and the asset, because the asset attached to the root node is generally not attached to other asset trees.

### Deleting a Node

The deletion of a node only deletes the node itself and does not delete the attached asset.

**Note**:  You cannot delete the node that has child node. Only the leaf node can be deleted.

1. In the EnOS Console, click **Asset Management** form the left navigation panel.
2. Select the root node and right click, then click **Delete node**.
3. In the pop-up windows, click **Confirm** to complete the deletion.


### Deleting a Instance

The deletion of a instance deletes the asset itself as well as all nodes that this asset is bound to.

**Note**：

 - You only can delete a instance when all nodes to that this asset is bound are leaf node.  
 - You cannot delete a instance if this asset is a connected device. You can delete a connected device via **Device Management**.

1. In the EnOS Console, click **Asset Management** form the left navigation panel.
2. Select the root node and right click, then click **Delete instance**.
3. In the pop-up windows, click **Confirm** to complete the deletion.
