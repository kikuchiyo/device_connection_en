## Creating a Protocol

EnOS Edge supports various communication protocols. This article instructs how to create a customized protocol.


### Procedure
You'll need to create a protocol and update the jar package of the protocol file.

1. In the EnOS console, click **Edge Gateway > Protocols** from the left navigation panel.    
2. Click **Create Protocol** and provide the following settings:

  - **Name** (required): The syntax of a completed name is _Protocol Type - Role – Name_.
    For a standard protocol, use the default _Std_ as the name. For example, if the protocol type is Modbus TCP, the role is Client, and the name is Std, the developer only needs to enter _Std_ in the **Name** filed, and the system will assemble the complete protocol name _Modbus TCP-Client-Std_.

  - **Type** (required): Select a protocol type from the drop-down list.

  - **Version** (required): The vision of this protocol.

  - **Jar package** (required): Click **Upload** to upload a jar package of the protocol that you created, which is going to be run on the EnOS Edge.

  - **Description** (required): The description of the protocol. Such as applied scenario.
