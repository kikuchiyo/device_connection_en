# Getting Started With Direct Device Connection

This article helps you quickly learn how to pre-configure direct connected devices to EnOS Cloud, how to send data from your device to EnOS Cloud, and how to check device communication information from EnOS Cloud.

## Scenario Description

For information on connection scenarios, please refer to "Scenario 2.2" mentioned in [Device Connection Scenarios](connection_scenarios).


## About This Task

Here we take the household PV inverter connection as an example. The inverter device triple is burned into the inverter collector during factory production. After powered on and connected to the network, the inverter, based on the device triple authentication, is directly connected to the cloud IoT Hub. The overall process is shown below:

  ![](media/device_connection_task_description.png)

Based on the above connection flowchart, the purposes to be achieved in this example are mainly as follows:
1. Create a device model
2. Create a product
3. Register the device
4. Simulate device sending data via device SDK
5. Check device communication status
6. Check device data


## Step 1: Create a Device Model

This step assumes that there is no device model to be reused. We create a new model named **Inverter_Demo** with the function defined as follows:

<table>
    <tr>
      <th>Function type</th>
      <th>Name</th>   
      <th>Identifier</th>   
      <th>Data Type</th>   
      <th>Data definition</th>   
    </tr>
    <tr>
      <td>Attribute</td>
      <td>Inverter type</td>     
      <td>invType</td>
      <td>enum</td>  
      <td>{0:Central,1:String}</td>      
    </tr>
    <tr>
     <td>Attribute</td>
      <td>Component capacity</td>
      <td>capacity</td>     
      <td>float</td>
      <td>kWp</td>      
    </tr>
    <tr>
      <td>Measure Points</td>
      <td>Active power</td>     
      <td>INV.GenActivePW</td>
      <td>float</td>  
      <td>kW</td>      
    </tr>
    <tr>
      <td>Service</td>
      <td>Control</td>     
      <td>INV.Control</td>
      <td>--</td>  
      <td>Invoke Method: Asynchronous</td>      
    </tr>
    <tr>
      <td>Event</td>
      <td>Error information</td>     
      <td>Error</td>
      <td>--</td>  
      <td>Event Type: Error</td>      
    </tr>
</table>

The steps to create this model are as follows:

1. In the EnOS Console, select **Access Management > Model Management**.
2. Click **New Model** at the top right of the page, and provide the following settings in the **Creating Model** window:
  - **Identifier**: Inverter_Demo
  - **Model Name**: Inverter_Demo
  - **Model Name (en)**: Inverter_Demo
  - **Category**: None
  - **Create From**: None
  - **Source model**: None
  - **Model Description**: Inverter model for demo project

  ![](media/model_inverter.png)

3. Click **Confirm** to complete the operation.
4. Click **View**, and click the **Feature Definition** tag in the "Model Details" screen.
5. Click **Add**, and provide the following settings in the **Add Feature** window:
  - **Attribute 1**
    - **Name**: Inverter Type/Inverter_Type
    - **Identifier**: invType
    - **Data Type**: enum
    - **Enum Items**:
      - Value: 0; Description: Central
      - Value: 1; Description: String
    - **Required**: Yes
  - **Attribute 2**
      - **Name**: Component capacity/Inverter_Capacity
      - **Identifier**: capacity
      - **Data Type**: float
      - **Unit**: kWp
      - **Required**: Yes
  - **Measure Point**
    - **Name**: Active power/Active_Power
    - **Identifier**: INV.GenActivePW
    - **Data Type**: float
    - **Point Type**: AI
    - **Unit**: kW
  - **Service**
    - **Name**: Control/Control
    - **Identifier**: INV.Control
    - **Invoke Method**: Asynchronous
    - **Input Parameters**:
      - Parameter Name: control
      - Identifier: control
      - Data Type: enum
      - Enum Items:
        - Value: 0; Description: Stop
        - Value: 1; Description: Start
    - **Output Parameters**:
      - Parameter Name: execResult
      - Identifier: execResult
      - Data Type: enum
      - Enum Items:
        - Value: 0; Description: Failure
        - Value: 1; Description: Success
  - **Event**
    - **Name**: Error information/Error
    - **Identifier**: Error
    - **Severity**: Error

For details on device model settings, please refer to [Creating Model](creating_model).


## Step 2: Create a Product

In this step, we create a product called **Inverter_Product**. We assume that the device of this product model sends data in JSON format and the data transfer is not encrypted using CA certificate.

1. In the EnOS Console, select **Access Management > Product Management**.
2. Click **New Product** at the top right of the page, and provide the following settings in the **Creating Model** window:
  - **Product Name**: Inverter_Product
  - **Asset Type**: Device
  - **Device Model**: Inverter_Demo
  - **Data Format**: Json
  - **Certificate-based Two-way Authentication**: Disable
  - **Product Description**: Inverter product for demo

  ![](media/create_product.png)

Filling specifications are as follows:
<table>
    <tr>
  		<th>Parameter
  		</th>
  		<th>Input Value
  		</th>      
  	</tr>
    <tr>
  		<td>Product Name
  		</td>
  		<td>The product name must be unique, supports Chinese characters, uppercase alphabets (A-Z), lowercase alphabets (a-z), numbers (0-9) and underline(_).
  		</td>      
  	</tr>
    <tr>
  		<td>Asset type
  		</td>
  		<td>Select a device
  		</td>
  	</tr>
    <tr>
  		<td>Device model
  		</td>
  		<td>Select a model that is already defined. If the selected model has not yet defined a feature, it can be set after the product is created.
  		</td>
  	</tr>
    <tr>
  		<td>Data Format
  		</td>
  		<td>JSON:
      Passthrough:
  		</td>
  	</tr>
    <tr>
  		<td>Product Description
  		</td>
  		<td>Product Name
  		</td>
  	</tr>
  </table>
3. Click **Confirm** to complete the operation.

For details on product settings, please refer to [Creating Products](creating_products).


## Step 3: Register the Device

In this step, we create a device named **INV001**, which belongs to the **Inverter_Product** product model created in the previous step.

1. In the EnOS Console, select **Access Management > Device Management**.
2. Click **New Device** at the top right of the page, and provide the following settings in the pop-up window:
  - **Product**: Inverter_Product
  - **Device Name**: INV001
  - **Inverter Type**: 0: Central, indicating centralized inverter
  - **Component Capacity**: 5.0
  - **Device Key**: Optional, generated automatically by system

  ![](media/register_device.png)

Filling specifications are as follows:
<table>
  <tr>
		<th>Parameter
		</th>
		<th>Description
		</th>
	</tr>
  <tr>
		<td>Product</td>
		<td>The product to which the device belongs. The displayed options vary according to the product configuration.
		</td>
	</tr>
  <tr>
		<td>DeviceName	</td>
		<td>The device name can be duplicated under the same product. For example: INV001.
		</td>
	</tr>
  <tr>
		<td>Devicekey</td>
		<td>
    Optional.
    When left blank, it will be automatically generated by the system.
    If you customize the setting, you need to ensure it is unique in the organization, and only supports uppercase alphabets (A-Z), lowercase alphabets (a-z), numbers (0-9), dash "-" and underline "_".
    </td>
  </tr>
  <tr>
    <td>Model Attribute</td>
    <td>The required attribute must be filled in when registering the device. The optional item can be added after the device is registered.
    </td>
  </tr>
</table>


## Step 4: SDK Simulates Device Sending Data

In this step, we send the inverter active power to the cloud through the device SDK simulation.

1. Obtain [Device Side SDK](https://github.com/EnvisionIot/enos-mqtt-java-sdk). For more information, please refer to the SDK's GitHub readme file.
2. Configure the EnOS Cloud connection address.
3. Configure the device triple, i.e. `ProductKey`,`DeviceKey`,`DeviceSecret`, obtained by the registered device into the sample connection program.
4. Modify the **postSubMeasurepoint** method, configure the name of the measure point that sending data. In this case, send the inverter active power point, set the point name **INV.GenActivePW** and the corresponding point value.

For specific SDK application, please refer to [SDK Device Side Connection](using_sdk).

## Step 5: Check the Device Connection Status

Go to the console and select **Connection Management > Device Management** to check the status of the INV001 device and confirm that the device is online.

  ![](media/device_status.png)


## Step 6: Check the Device Data

Go to the console, select **Connection Management > Device Management**, then go to **Device Details**, open the **Measure Point** tab, and select a measure point, click **View Data** to check the data history record.
