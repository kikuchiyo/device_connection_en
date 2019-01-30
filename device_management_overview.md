# About Device Management

EnOS™ Device Management helps you quickly and securely connect physical devices to EnOS Cloud and start to transfer data, manage device lifecycle, and map the physical asset structure to the digital world.


## Key Personas

EnOS Device Management Service primarily serves the following roles:

**IoT Engineer**

IoT Engineer, who performs the on-site installation, including installing the edge gateway devices and connecting the cables between edge gateways and devices, sets up device connections, and debugs the communication between the devices and the cloud.

**Edge Developer**

Edge Developer, who develops the MQTT client applications of the edge according to the EnOS standard device protocols. The goal of the applications is to collect the telemetry data of the edge and transfer the data through supported protocols to the EnOS Cloud in the supported formats.

**Asset Manager**

Assets Manager, who creates and manages the asset hierarchy (asset tree) based on the business case scenarios.

**Application Developer**

Application Developer, who develops applications to acquire device telemetry and configuration information via EnOS APIs and SDKs to fulfill requirements of certain business case scenarios.


## Key Capabilities

### Device Modelling

Allows devices of thousands of models from different manufacturers to be unified into a small number of common models and thus facilitates application processing. EnOS™ Cloud has accumulated a large set of device models in its model library to facilitate abstraction of your asset data. [Learn more >>](model/model_overview)

### Device Provisioning

Helps you establish connection from the devices to EnOS Cloud, secure the two-way communication between the devices and the cloud, and manage the device lifecycle. [Learn more >>](deviceconnection_overview)

### Asset Alerts

Enables you to define, receive, and process alerts for your organization assets. The service also allows you to define alert triggering rules against the asset data, to achieve real-time alarming and troubleshooting. [Learn more >>](https://www.envisioniot.com/docs/event-management/en/latest/alert_overview.html)

### Asset Management

Enables asset owners, who understand the enterprise asset management business, to quickly create the asset topology to manage assets in the cloud in terms of different dimensions. [Learn more >>](asset_tree/assettree_overview)


## Related Services of EnOS Device Management

### Stream Analysis Service

Stream Analysis enables you to define the asset calculation logic, subscribe to the asset data, and perform data calculations based on the predefined calculation logic for your organization. For example, calculating a 5-minute average of the measurement points or a 10-minute average, and etc. [Learn more >>](https://www.envisioniot.com/docs/online-data/en/latest/streaming_overview.html)


## Next Steps

Learn how to quickly provision a typical smart IoT device on EnOS Cloud and start to sending telemetries between the device and the cloud:

- [Getting Started With Direct Device Connection (Without Edge)](gettingstarted_device_connection)

Learn how to provision a traditional industry equipment that connects through an edge gateway:

- [Getting Started With Connecting Sub-device to EnOS Cloud via Edge](gettingstarted_edge_connection)
