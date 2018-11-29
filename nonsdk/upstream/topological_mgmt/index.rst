Device topology management
=============================
After a sub-device is registered to the EnOS Cloud, the edge reports the
topological relationship of the edge and sub-devices to the EnOS Cloud
before the sub-device connects to cloud. EnOS Cloud verifies the
identity of the device and the topological relationship during
connection. If the verification is successful, EnOS cloud establishes a
logical connection to the sub-device and associates the logical
connection with the physical connection of the edge.

.. toctree::
   :maxdepth: 1

   add_topological
   delete_topological
   get_topological
