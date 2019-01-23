# Adding an EnOS Edge Gateway

The Edge gateway needs to be configured before connect the sub-device to the edge gateway. This article describes how to configure edge gateway in order to establish the connection between edge gateway and the sub device.

## Before You Start

1. You must have obtained the serial number (SN) of the Edge gateway.

2. You must have completed the initialization of the Edge gateway. The initialization of the Edge gateway hardware is usually done by the Envision project team. For more information, consult the Envision project manager.


## Step 1: Adding the Edge Gateway

1. In the EnOS console, click **Edge Gateway > Edge Management** from the left navigation panel.    

2. Click **Add**.

3. In the pop-window, enter the name and serial number of the Edge gateway.

4. Click **Save** to complete creating Edge gateway.

After the Edge gateway is successfully added, in the **Edge Management** page, you can view the name, SN, version, the current communication status, and the publish status of each Edge, as shown in below figure:

.. image:: media/imageN001.png
   :width: 800px

## Step 2: Connecting the Sub-device to the Edge Gateway

After the Edge gateway is added, you can connect the sub-device to the edge gateway.

1. Click **Connect Devices** after the Edge gateway to be connect to open the configuration page.

2. In the configuration page, you must finish the following configuration in order to establish the connection between the sub-device and the edge gateway.

### Adding Connection

Firstly, you need to configure the connection for the Edge gateway.

According to the actual needs, multiple connections can be added under one Edge gateway, and the connection method must be selected according to the type of the protocol.

1. Click **Add Connection** next to the **Non-Direct Connections**.

2. In the pop-up window, enter the name of the connection, select the connection mode, and set the connection parameters according to the selected connection method.

   .. note:: Usually the Edge is not connect directly to the end server or device. Instead, the edge is connect to a network gateway, and then connect to the end server or device via this network gateway. Therefore, you need to know the mapping relationship between the IP address and port number of the network gateway and the edge gateway.

As shown in the following figure, Edge is used as the TCP/IP client, so the configured connection parameters are the IP address and port number of the server.

.. image:: media/image011.png
   :alt: Figure: Example of Adding Connection
   :width: 700px

### Adding Devices

After adding connection, the next step is to add device to this connection.
In this step, you'll add the device and configure the basic information.

**Step 1: Add Devices**

1. Click **Add Device** next to the connection.

   .. image:: media/image012.png
      :alt: Figure: Add Devices to the Connection
      :width: 700px

2. In the pop-up window,

   - select the product to which you want to add the devices.
   - select the devices you want to add.
   - select the device template that the device needs to be associated with.

     .. note:: You must first select the same kind of devices, then you can select the device template that the devices to be associated with.

   The device template is used as the device communication driver, which includes the device communication point table, communication protocol, protocol configuration file and other information. For more information, see [Creating and Managing Device Templates](managing_templates)

3. Click **Save** to add the device.

**Step 2: Update Basic Information**

If the basic information of the added device needs to be updated, you can modify the information in the following approach:

1. Click **Export** next to device connection to export the device connection information table.

2. Update the basic information in device connection information table .
3. Click **Import** to upload the information table.

You can find the **Import** and **Export** button as shown below:

.. image:: media/image014.png
   :width: 700px



<!--![](media/image015.png)

*Figure: Device Connection Information Table*-->

<!--Click the **Delete** button next to the device to remove this device from the connection. To delete devices in batch, check the devices you want to delete under this connection, and click the “Bulk Delete” button.-->

### Configuring Logical Addresses or Offsets

Since multiple devices are connected under one connection, the logical address and corresponding offset must be configured for each device. The configuration of each device depends on the communication protocol used and its settings.

You can configure the device by two ways:
- One by one.
- In batches by updating device connection information table.

**Configure the device one by one in the following approach:**

1. Click **Edit** after the device to be edit.

2. Edit the configuration according to your requirement and then click **OK**.

   .. image:: media/image020.png
      :alt: Figure: Configure Logical Addresses and Offsets on a Device-by-Device Basis
      :width: 700px

**You can configure the device in batches in the following approach:**

1. Click **Export** after the device connection to download the device connection information table.

2. Edit the device connection information table according to your requirement.

   The table supports the configuration of the AI, DI, PI, AO, DO, and PO offsets. The basic configuration method is use dash-connection, such as `0-50`, when there are multiple offsets, you can use `#` to separate multiple values, such as `0-50#1000-1050`.

3. Click **Import** to upload the information table.

### Publishing Configuration

After completing the above configurations, you need to publish the configuration to the Edge.

Click **Publish** to publish the configuration to the corresponding edge gateway and view the publish status. The configuration will not take effect until it is published.

You can find the **Publish** button and the publish status as shown below:

.. image:: media/image021.png
   :width: 700px

## Step 3: Testing Communication

After completing and publishing the configuration to the edge gateway, you need to check whether the configuration is correct. In the connection configuration page, a communication indicator is provided. When the device connection is normal in the transmission layer (TCP/IP layer), the indicator is green, otherwise it is red.

.. image:: media/image022.png
   :alt: Figure: Communication Status Indication Icon on Transport Layer
   :width: 700px

There are several reasons for communication interruption, including but not limited to the following reasons:

- Configuration is not published
- Configuration error
- The site end communication is abnormal.

Therefore, further debugging is needed to help you locate the problem. EnOS Edge provides communication testing functionality to help achieve this goal.


**You can debug the communication in the following approach:**

1. Click **Test**  after the device connection to open the batch test page.

2. In the connection debugging page, you can:

   - Switch connections by using the drop-down menu.
   - Activate or pause the communication test features by clicking the **Start/Pause** button.

.. image:: media/image026.png
   :alt: Figure: Bulk Communication Test Overview
   :width: 700px

Batch testing provides four features: data, datagram, log, and console. Click the corresponding tab to switch among the different features, the operations of each page are described in the below sections:

### Data

In the **Data** tab, you can view all the devices under this connection, filter the devices to see the update of the collection point data and set numbers for telemetry and telecommand points:

.. image:: media/image029.png
   :alt: Figure: Data Feature Overview
   :width: 700px

**Setting number**

You can set numbers for the telemetry and telecommand points in the following approach:

1. Click **Set** to set the value.

2. click **Send** to send the set value to the cloud. Click once to send one time, it will not interrupt the upload of the original data, equivalent to inserting a value to the cloud.

.. image:: media/image030.png
   :alt: Figure: Number Setting Feature
   :width: 700px

### Datagram

In the **Datagram** tab, you can view and copy the incoming and outgoing datagram.

### Log

In the **Log** tab, to avoid flooding of information, the system hides the logs of info types and only displays logs of warning and error types to assist the user in diagnosing the cause of the communication error.

### Console

In the **Console** tab, you can debug through the common communication debugging commands. The most frequently used debugging commands are including:

- Test basic ping test (You'll need to enter the IP address of the ping in the input box)
- Check local IP
- Telnet Test(You’ll need to enter the IP and port number.)
- Check TCP connection

.. image:: media/image033.png
   :alt: Figure: Console Feature Overview
   :width: 700px

### Testing the Communication of a Single Device

You can test the communication on a single device and view the corresponding data.

1. Click **View** after the device to be tested.

2. In the pop-up window, you can test the view the detailed information and set the telemetry and telecommand points which the operations are same as the bulk communication test.

.. image:: media/image034.png
   :alt: Figure: Single Device Communication Test Feature
   :width: 700px

## Summary

After the connection configuration of the sub-devices is completed in the Edge gateway, the data of these sub-devices is automatically sent to the EnOS cloud.
