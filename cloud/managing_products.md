# Managing Products

On the Products screen, you can perform operations such as turning on dynamic registration, viewing device logs, and debugging devices.

## Turning On Dynamic Registration

On the Product Details screen, you can turn on dynamic registration to support batch burning for devices of the same product model. By doing so, you can batch burn the same productKey and productSecret to multiple devices, and these devices will be activated dynamically if they go online.

1. In the EnOS Console, select **Access Management > Product Management**.
2. Click **View** next to the product to open the **Product Details** page; choose the **Product Info** tab and turn on **Dynamic Registration**.

## Viewing Logs

On the Product Details screen, you can view the logs of important behaviors of all the devices under the product.

1. In the EnOS Console, select **Access Management > Product Management**.
2. Click **View** next to the target product to open the **Product Details** page, and choose the **Log Service** tab.
3. On the **Device Behavior Analysis** tab, enter the target device and set a time period to view the log of that device for the set period of time.
4. (Optional) To view logs of uplink and downlink messages, click the **Uplink Message Analysis** and **Downlink Message Analysis** tabs.
  - The **Uplink Message Analysis** page mainly displays the logs of the following uplink messages:
    - Messages sent by the device to the topic queue
    - Messages flowed from the topic queue to the rules engine
    - Messages forwarded from the rules engine to other services and applications in the EnOS Cloud
  - The **Downlink Message Analysis** page mainly displays the logs of messages sent from the cloud to the device.
  <!--This requires a list of error codes-->

## Debugging Online Devices

On the Product Details screen, you can debug devices under the product, simulate a real device to connect to the cloud, report defined attributes, and handle events. Based on the data of the simulated device, the cloud can complete app development and debugging. Once the real device is online, the virtual device will automatically go offline.

1. In the EnOS Console, select **Access Management > Product Management**.
2. Click **View** next to the target product, and choose **Online Debugging**.
3. Select the device you want to debug in the upper left corner.
4. Simulate a scenario using the debugging feature.
5. Click the **Send** command.

<!--Ask Xu Wei for a list-->
