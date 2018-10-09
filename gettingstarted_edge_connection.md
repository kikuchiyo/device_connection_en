# Getting started with device connection through EnOS™ Edge

For traditional devices that do not support MQTT protocol, you can use EnOS™ Edge to connect your devices into EnOS™ Cloud.

## Step 1: Apply for an edge


Apply for an edge from the Envision project manager<!--edge申请没有对外开放-->.

You'll receive a serial number that you'll later use for activating your edge.

## Step 2: Create sites and devices

In EnOS™, the devices and the organization entity where the
devices belongs to are managed as *assets*. You'll first need to create your devices and sites in EnOS™.

Use the **Asset Management > Sites and Devices** function to create sites and associate devices into your sites. For more information, see [Creating sites and devices](asset_management/creating_sites_devices.md).

## Step 3: Organize sites

In practice, devices are typically organized hierarchically.
The hierarchical structure is an *asset tree*. For more information about the asset management mechanism of EnOS™, see [Asset management overview](asset_management/asset_overview).

Use the **Asset Management > Asset Tree** function to arrange your sites hierachically according to their organization in the real world. For more information, see [Creating asset tree](asset_management/creating_asset tree.md).

## Step 4: Create templates that adapts device models to real devices
Device templates, which play as the adaptor between device models and real devices, mainly define the communication protocol and mapping relationship between the data acquisition point and device model point.

Use the **Templates** function to create templates for your devices. For more information, see [Creating a template](asset_management/creating_templates).

## Step 5: Activate the edge and configure the

Use the **Edge Connection** function to activate your edge. Enter the edge serial number getting from Envision project manager and then activate it.

## Step 6: Configure the edge connection and add devices into the edge connection

The major procedure is as follows.

1. Define the edge connnection parameters, such as IP address, Port, connection mode, short or long connection.
2. Add devices into relevant edge connection.
3. Bind templates for devices.
4. Configure the logical address or offset

For details, see [Configuring edge connection](asset_management/configuring_edge_connection).
