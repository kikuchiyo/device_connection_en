# Managing Asset Trees

This article describes the asset tree management operations.

## Before You Start

To perform the management operations, you must have write access to the **Asset Tree** service. If you don't have the access, contact your OU administrator to obtain the access. For more information about user access in EnOS, see [Policy, Roles, and Access](/docs/iam/en/latest/access_policy).

### Deleting an Asset

Click the |delete| button next to an asset to delete it. Before deleting an asset, make sure it does not contain any asset bound to it.

.. |delete| image:: ../../media/button_delete_asset.png

.. image:: ../../media/deleting_asset.png

By deleting an asset, you only deletes its association to the asset tree, not the device represented by the asset, which is created in **Device Management** .

## Deleting an Asset Tree

Select **Delete** under **Delete Asset Tree**.

Make sure no child assets exist under the asset tree before deleting the asset tree.

.. image:: ../../media/deleting_asset_tree.png

## Moving a Node

You can move any node on an asset tree except the tree itself. Click and drag the |move| button to move it. If your destination is deeper than Layer 7 of a tree, the move operation fails. By moving a node, all assets bound to it as sub-nodes will also be moved to the new location.

.. |move| image:: ../../media/button_move_asset.png

<!--end-->



