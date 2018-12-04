# Getting Started With Connecting Sub-device to EnOS Cloud via Edge

This article helps you quickly learn how to pre-configure the sub-device and Edge to the EnOS Cloud, allowing the sub-device to connect and send data to the EnOS Cloud through the Edge, as well as how to view the communication information between the device and Edge from the EnOS Cloud.


## Scenario Description
For information on connection scenarios, please refer to "Scenario 1.2" mentioned in [Device Connection Scenarios](connection_scenarios).


## About This Task

In this example, an inverter will be connected to the EnOS Cloud through the Edge. Edge will collect data from the inverter and send them to the EnOS Cloud as a proxy. The overall connection scenario is shown in the figure below:

  ![](media/edge_connection_task_description.png)

Based on the above connection flowchart, the purposes to be achieved in this example are mainly as follows:
1. Create a device model
  - Gateway model
  - Inverter Model
2. Create a product
  - Gateway product
  - Inverter product
3. Register the device
  - Gateway device
  - Inverter device
4. Gateway configuration
  - Access data using EnOS Edge
  - Use the device SDK to simulate gateway sending data as a proxy of the sub-device
5. Check device communication status
6. Check device data


## Prerequisites

Before proceeding with this example, make sure that you have read [Getting Started With Direct Device Connection](gettingstarted_device_connection).
In this example, we only create models, products, and devices of the gateway device. For configuration of the inverter device, please also refer to **Getting Started With Direct Device Connection**


## Step 1: Create a Device Model

We will create an Edge device model called **Edge_Model** in this step, as we assume that there are no reusable Edge models.

1. In the EnOS Console, select **Access Management > Model Management**.
2. Click **New Model** at the top right of the page, and provide the following settings in the **Creating Model** window:
  - **Identifier**: Edge_Model
  - **Model Name**: Edge_Model
  - **Category**: None
  - **Create From**: None
  - **Source model**: None
  - **Description**: Edge Model

  ![](media/model_edge.png)

3. Click **Confirm** to complete the operation.
4. Click **View**, and click the **Feature Definition** tag in the "Model Details" screen.
5. Click **Add**, and provide the following settings in the **Add Feature** window:
  - **Attributes**
    - **Name**: version
    - **Identifier**: version
    - **Data Type**: string
    - **String Length**: 20
    - **Required**: Yes

For details on device model settings, please refer to [Creating Model](creating_model).


## Step 2: Create a Product

In this step, we will create a product called **Edge_Product**. The Edge device of this product model will send data in JSON format to the EnOS Cloud.

1. In the EnOS Console, select **Access Management > Product Management**.
2. Click **New Product** at the top right of the page, and provide the following settings.
  - **Product Name**: Edge_Product
  - **Asset Type**: Gateway
  - **Device Model**: Edge_Product
  - **Data Format**: Json
  - **Certificate-based Two-way Authentication**: Disable
  - **Product Description**: Edge Product

3. Click **Confirm** to complete the operation.

For details on product settings, please refer to [Creating Products](creating_products).


## Step 3: Register the Gateway

In this step, we create an edge device named **Edge01**, which belongs to the **Edge_Product** product model created in the previous step.

1. In the EnOS Console, select **Access Management > Device Management**.
2. Click **New Device** at the top right of the page, and provide the following settings in the pop-up window:
  - **Product**: Edge_Product
  - **Device Name**: Edge 01
  - **Version**: Optional, left blank by default
  - **Device Key**: Optional, generated automatically by system

![](media/register_edge.png)


## Step 4: Gateway Configuration

### Access Data Using EnOS Edge
> Note: This step only applies to scenarios using EnOS Edge provided by Envision. If the gateway products are from other vendors, please refer to their respective gateway configuration instructions.

1. Apply to the manager of Envision project for an Edge gateway device, and you will obtain an SN for the Edge gateway.
2. Go to the Edge gateway configuration page, and add an Edge gateway device (enter the obtained SN)
3. In the Edge gateway, configure its connection with the sub-device.
4. Publish the configuration to the Edge gateway.

For more information on how to configure the EnOS Edge gateway, please refer to [Edge Gateway Configuration](https://docs.envisioniot.com/docs/enos-edge/zh_CN/latest/edge_overview.html)



### Use the Device SDK to Simulate Gateway Sending Data as a Proxy of the Sub-device
In this step, we send the inverter active power to the cloud through the device SDK simulation.

1. Acquire the [device SDK](https://github.com/EnvisionIot/enos-mqtt-java-sdk). For more information, please refer to the SDK's GitHub readme file.
2. Configure the EnOS Cloud connection address.
3. Configure the trigraph of main gateway and sub-devices (`ProductKey`, `DeviceKey`, `DeviceSecret`) into the sample connection program.
4. Modify the **postSubMeasurepoint** method, configure the name of the measure point that sending data. In this case, send the inverter active power point, set the point name **INV.GenActivePW** and the corresponding point value.
5. Method for invoking the sample:
  - Online gateway
  - Gateway adds the topology of sub-device
  - Gateway goes online as a proxy of the sub-device
  - Gateway sends data as a proxy of the sub-device

For specific SDK application, please refer to [SDK Device Side Connection](using_sdk).


## Step 5: Check the Device Status

Go to the console and select **Connection Management > Device Management** to check the status of the Edge01 and INV001 devices and confirm that the devices are online.


## Step 6: Check the Device Data

Go to the console, select **Connection Management > Device Management**, then go to **Device Details**, open the **Measure Point** tab, and select a measure point, click **View Data** to check the data history record.
