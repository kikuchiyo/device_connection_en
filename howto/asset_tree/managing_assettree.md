# Managing Asset Trees

This article describes the asset tree management operations from two aspects: asset and node.

- The operations of the node only affect the node.
- The operations of the asset affect all nodes that the asset is attached to.


## Before You Start

To performe the management operations, you must have write access to the **Asset Tree Management** service. If you don't have the access, contact your OU administrator to obtain the access. For more information about user access in EnOS, see [Policy, Roles, and Access](/docs/iam/en/dev/access_policy).

## Deleting Asset Tree

Deleting an asset tree is accomplished by deleting the root node of the asset tree. You can delete a root node in the following approaches:

- Delete node
- Delete asset

  For a root node, we recommend using **Delete asset**, which will delete both the node and the asset, because the asset attached to the root node is generally not attached to other asset trees.

### Deleting a Node

The deletion of a node only deletes the node itself and does not delete the attached asset.

.. note:: You cannot delete the node that has child node. Only the leaf node can be deleted.

1. In the EnOS Console, click **Asset Tree** form the left navigation panel.

2. Expand the asset tree, right-click on the root node, and select **Delete node**.

3. In the pop-up windows, click **Confirm** to complete the deletion.

### Deleting an Asset

The deletion of an asset deletes the asset itself as well as all nodes that this asset is bound to.

.. note:: - You only can delete an asset when all nodes bound to the asset are leaf nodes.  
   - You cannot delete an asset if this asset is a connected device. You can delete a connected device via **Device Management**.

1. In the EnOS Console, click **Asset Tree** form the left navigation panel.

2. Expand the asset tree, right-click on the root node, and select **Delete asset**.

3. In the pop-up windows, click **Confirm** to complete the deletion.
