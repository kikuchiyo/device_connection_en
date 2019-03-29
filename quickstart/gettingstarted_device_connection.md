# Connecting a Smart Device into EnOS Cloud

This article helps you quickly learn how to provision a direct-connecting device to the EnOS Cloud, how to send device telemetry, and how to check device communication state from the EnOS Console.

## About the Scenario

For information about the connection scenario of this task, see "Scenario 1.1" in [Device Connection Schemes](../learn/connection_scenarios).

## About This Task

Here we take the household PV inverter connection as an example. The inverter device triple is burned into the inverter during manufacturing. After you power on and connect the inverter to the network, the inverter is connected to the IoT Hub based on the device triple authentication. The overall process is shown below:

.. image:: ../media/device_connection_task_description.png

As shown in the flowchart above, the procedure falls into the following steps:

1. Create a device model for the inverter

2. Create a product for the inverter

3. Register the inverter

4. Simulate the inverter to send data via device SDK

5. Check device communication status

6. View device data

## Step 1: Create a Device Model

This step assumes that there is no device model to be reused. We create a new model named **Inverter_Demo** with the features defined as follows:

.. list-table::
   :widths: auto

   * - Feature Type
     - Name   
     - Identifier   
     - Data Type   
     - Value   
   * - Attribute
     - Inverter type     
     - invType
     - enum  
     - {0:Central,1:String}      
   * - Attribute
     - Component capacity
     - capacity     
     - float
     - kWp      
   * - Measure Point
     - Active power     
     - INV.GenActivePW
     - float  
     - kW      
   * - Service
     - Control     
     - INV.Control
     - \
     - Invoke Method: Asynchronous
   * - Event
     - Error information
     - Error
     - \
     - Event Type: Error

The steps to create this model are as follows:

1. In the EnOS Console, click **Model** from the left navigation panel.

2. Click **New Model**, and provide the following settings in the **New Model** window:

   - **Identifier**: Inverter_Demo
   - **Model Name**: Inverter_Demo
   - **Model Name (en)**: Inverter_Demo
   - **Category**: NA
   - **Create From**: No
   - **Support Passthrough**: Default
   - **Source Model**: NA
   - **Description**: Inverter model for demo project

3. Click **OK** to complete the operation.

   .. image:: ../media/model_inverter.png

4. Click **Edit**, and click the **Feature Definition** tab in the **Model Details** screen.

5. Click **Add**, and provide the following settings in the **Add Feature** window:

   - **Attribute 1**

     - **Name**: Inverter_Type
     - **Identifier**: invType
     - **Data Type**: enum
     - **Enum Items**:
       - Value: 0; Description: Central
       - Value: 1; Description: String
     - **Required**: Yes

   - **Attribute 2**

     - **Name**: Inverter_Capacity
     - **Identifier**: capacity
     - **Data Type**: float
     - **Unit**: kWp
     - **Required**: Yes

   - **Measure Point**

     - **Name**: Active_Power
     - **Identifier**: INV.GenActivePW
     - **Data Type**: float
     - **Point Type**: AI
     - **Unit**: kW

   - **Service**

     - **Name**: Control
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
     - **Name**: Error
     - **Identifier**: Error
     - **Severity**: Error

6. Click **OK** to complete the operation.

For details on device model settings, see [Creating Model](../howto/model/creating_model).


## Step 2: Create a Product

In this step, we create a product called **Inverter_Product**. We assume that a device of this product model sends data in JSON format and the data transmission is not encrypted using CA certificate.

1. In the EnOS Console, select **Device Management > Product**.

2. Click **New Product**, and provide the following settings in the **New Product** window:

   - **Product Name**: Inverter_Product
   - **Asset Type**: Device
   - **Device Model**: Inverter_Demo
   - **Data Format**: Json
   - **Certificate-based Two-way Authentication**: Disable
   - **Product Description**: Inverter product for demo

3. Click **OK** to complete the operation.

   .. image:: ../media/create_product.png

For details about product settings, see [Creating Products](../howto/device/manage/creating_product).


## Step 3: Register the Device

In this step, we create a device named **INV001**, which belongs to the **Inverter_Product** product model created in the previous step.

1. In the EnOS Console, select **Device Management > Device**.

2. Click **New Device**, and provide the following settings in the **New Device** window:

   - **Product**: Inverter_Product
   - **Device Name**: INV001
   - **Use DST**: No
   - **timezone**: UTC+14:00
   - **Inverter Type**: 0: Central, indicating centralized inverter
   - **Inverter Capacity**: 5.0
   - **Device Key**: Optional, generated automatically by system

3. Click **Confirm** to complete the operation.

   .. image:: ../media/register_device.png   

For details about device settings, see [Creating a Device](../howto/device/manage/creating_device).

After you complete the device registration, obtain the device triple: `ProductKey`,`DeviceKey`,and `DeviceSecret`, which will be used in the following step.

## Step 4: Use Java SDK to Simulate Device Sending Telemetry

In this step, we use the sample code of Java SDK to simulate sending the inverter active power to the cloud.

1. Obtain the [Device SDK](https://github.com/EnvisionIot/enos-mqtt-java-sdk). For information about how to set up the development environment, see the GitHub readme file.

2. Configure the EnOS Cloud connection as instructed in the readme file.

3. Configure the address of the EnOS cloud (`environment_address`) and the device triple (`ProductKey`,`DeviceKey`,`DeviceSecret`) into the sample connection program. The device triple is obtained when you register the device.

   ```java
   public static void initWithCallback() {
        System.out.println("start connect with callback ... ");

        try {
            client = new MqttClient(environment_address, productKey, deviceKey, deviceSecret);
            client.getProfile().setConnectionTimeout(60).setAutoReconnect(false);
            client.connect(new IConnectCallback() {
                public void onConnectSuccess() {

                    System.out.println("connect success");
                }

                public void onConnectLost() {
                    System.out.println("onConnectLost");
                }

                public void onConnectFailed(int reasonCode) {
                    System.out.println("onConnectFailed : " + reasonCode);
                }
            });
        } catch (EnvisionException var1) {
        }

        System.out.println("connect result :" + client.isConnected());
   }
   ```

4. Modify the `postSubMeasurepoint` method, configure the name of the measure point that sends telemetry to the cloud. In this example, we send the active power point of the inverter, set the point name **INV.GenActivePW** and the corresponding point value.

   ```java
   public static void postMeasurepoint() {
        Random random = new Random();
        System.out.println("start post measurepoint ...");
        MeasurepointPostRequest request = (MeasurepointPostRequest)MeasurepointPostRequest.builder().addMeasurePoint("invGenActivePW", random.nextDouble()).build();
        try {
            client.fastPublish(request);
            System.out.println(" post measurepoint success...");
        } catch (Exception var3) {
            var3.printStackTrace();
        }

   }
   ```

5. Use the `handleServiceInvocation()` method to handle the service invocation request from the cloud.

   ```java
   public static void handleServiceInvocation() {
        IMessageHandler<ServiceInvocationCommand, ServiceInvocationReply> handler = new IMessageHandler<ServiceInvocationCommand, ServiceInvocationReply>() {
            public ServiceInvocationReply onMessage(ServiceInvocationCommand request, List<String> argList) throws Exception {
                System.out.println("rcvn async serevice invocation command" + request + " topic " + argList);
                return (ServiceInvocationReply)ServiceInvocationReply.builder().addOutputData("execResult", 0).build();
            }
        };
        client.setArrivedMsgHandler(ServiceInvocationCommand.class, handler);
    }
    ```

For more information, see [Using the Device SDK](../howto/device/develop/using_java_sdk).

## Step 5: Check the Device Connection Status

In the EnOS Console, click **Device Management > Device**, locate the device and check the status of the INV001 device and confirm that the device is **Online**.

.. image:: ../media/device_status.png

## Step 6: Check the Device Data

1. In the **Device** page, locate the device and click **View** to show the **Device Details** page.

2. Click the **Measure Points** tab, and select the **INV.GenActivePW** measure point, click **View Data** to view the historical data.

## Step 7: Use Online Debugging Tool to Set Measure Point Value

1. Click **Device Management > Product**, Click **View** for the product that the device belongs to.

2. In the product details page, click **Debugging**。

3. Select the device to debug.

4. Select the model point from the **Debugging** drop-down list and the **Method** to use. In this example, we select to **SET** the **INV.GenActivePW** point, and click **Run**.

   .. image:: media/debug_postmeasurepoint.png

When the value of the measure point is set successfully, you'll receive response similar to the following from your Java development environment:

```
AnswerableMessageBody{id='21', method='thing.service.measurepoint.set', version='1.0', params={invGenActivePW=2.0}}
```

<!--end-->
