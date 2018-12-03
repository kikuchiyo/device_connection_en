# Device Connection Scheme

On the EnOS platform, unified authentication and online steps must be performed by the EnOS on both the Edge devices and devices connected directly to the IoT Hub before data can be sent to the platform.

EnOS mainly provides the following connection schemes:
- The device is directly connected into and communicate with the IoT Hub without using gateway, i.e. edge in our scenario, to complete the authentication and data reporting. The device connected via this solution is called _directly connected device_.
- The device is connected to the EnOS IoT Hub via edge. The device connected via this solution is called _sub device_. The gateway serves as a proxy of the sub devices to help them complete operations, including authentication, connecting to Internet, and data transmission.

The connection scheme is usually selected according to the hardware capabilities of the device and the security requirements for the device connection.

## Connection Schemes

Internet of Everything (IoE), provided that the object has the ability to be connected, that is, it should at least meet the following two requirements:
- Has the ability to be connected
- Supports burning of firmware and running of connection program

According to the above attributes, real-world devices can be divided into two main categories:
- Those support firmware burning, as well as direct connection to the IoT platform via Wi-Fi, GPRS, 3G, or 4G signals.
- Those do not support firmware burning, and are lack of the ability to connect via Wi-Fi, 3G, or 4G. In this scenario, data of these devices need to be collected by an edge gateway, and the devices are connected to the IoT platform through the edge gateway. Edge needs to support firmware burning and networking.

### Scenario of Direct Device Connection

The devices can be connected directly to the cloud. Some common devices include:
- Devices with smart acquisition rod, such as household inverters, and household energy storage batteries.
- Smart home devices, such as surveillance cameras, and smart thermometers and hygrometers.

### Scenario of Gateway Proxy Connection
The devices need a gateway proxy to connect to the cloud. Some common devices include:
- Distributed inverters: the gateway collects data directly from multiple inverters and then sends the data to the cloud.
  ![](media/inverter_gateway.png)

- SCADA: the SCADA is connected directly to the wind turbine and collects the data; the gateway is connected with the SCADA to collect its data, and then sends the data to the corresponding wind turbine device instance in the cloud.
  ![](media/turbine_scada_gateway.png)

## Security Authentication Options

There are two security authentication methods:
- Secret-based one-way authentication: one-way authentication with weak security, used by the system by default.
- Certificate-based two-way authentication: two-way authentication with high security, enabled actively by the user.

For more information on the authentication mechanism for device connection security, please refer to [Device Authentication Mechanism](deviceconnection_authentication).

## Message Flow

<table>
   <tr>
     <th>Scenario Number</th>
     <th>Union method</th>
     <th>Activation Mode</th>
     <th>Whether SA is Used</th>

   </tr>
   <tr>
     <td>1.1</td>
     <td>Connect via Gateway</td>
     <td>Static Activation via Device Secret</td>
     <td>Yes</td>

   </tr>
   <tr>
     <td>1.2</td>
     <td>Connect via Gateway</td>
     <td>Static Activation via Device Secret</td>
     <td>No</td>

   </tr>
   <tr>
     <td>2.1</td>
     <td>Direct Connection</td>
     <td>Static Activation via Device Secret</td>
     <td>Yes</td>

   </tr>
   <tr>
     <td>2.1</td>
     <td>Direct Connection</td>
     <td>Static Activation via Device Secret</td>
     <td>No</td>

   </tr>
   <tr>
     <td>2.3</td>
     <td>Direct Connection</td>
     <td>Dynamic Activation via Product Secret</td>
     <td>No</td>
   </tr>
 </table>

The message flow of different connection and activation methods is depicted in the following figures:

### Connect via Gateway

![Device connection overview](media/overview_device_connection_2_0_v3_1.png)


#### Scenario 1.1: The connected sub-device is not registered; it is dynamically registered through the Edge

1. In the EnOS Console, the Edge developer registers an Edge app on the EnOS Cloud, and obtains the app's service account (SA): the `accessKey` and `accessSecret`.

2. The IoT implementer needs to log in to the EnOS Console and performs the following configurations under Customer Organization:
  - Creates an Edge product and registers the Edge device to obtain the Edge device trigraph.
  - Creates a product of device to be connected to the Edge and obtains the `productkey`.

3. The following credential information needs to be burned into the Edge before it leaves the factory:
  - The SA of the Edge app to gain access to the EnOS API.
  - The Edge device trigraph issued by the EnOS Cloud.
  - The `productkey` of the device that needs to be connected to the Edge, and the organization identification (`orgId`) of the device.

4. The EnOS Cloud performs the following authentication when the Restful interface is called by the Edge:
  - The Edge uses the SA to gain access to the EnOS API. If the service account is incorrect, the Edge will not be able to call the EnOS API and the authentication will fail.
  - The EnOS Cloud uses IAM to verify the parameter orgId and parameter SA carried in the Edge connection request, and checks whether the corresponding organization (orgId) has registered an Edge app. If no Edge app is registered, the authentication will fail.
  - The EnOS Cloud verifies the attribution between the two request parameters orgId and `productkey`. If the product corresponding to the `productkey` does not belong to the organization corresponding to the orgId, the verification will fail.

5. The EnOS Cloud performs authentication on the Edge device
  - By default, the Edge enables the secret-based one-way authentication. The Edge carries the trigraph and connects to the cloud, in where an authentication will be performed on the Edge trigraph, then the device is allowed to log in if the authentication is successful.
  - The Edge device will be activated upon its first login, and its status will be updated from inactive to online.

6. If the certificate-based two-way authentication is enabled, the generation and distribution of the certificate will be carried out as follows:
    - The Edge Configuration Center initiates a certificate request, which carries the certificate request file, to the EnOS IoT Hub.
    - The EnOS IoT Hub proxy forwards the request to the EnOS Certificate Service.
    - The Certificate Service generates a certificate and returns it to the IoT Hub.
    - The IoT Hub records the certificate associated with the Edge, and returns the certificate to the Edge.

7. The IoT implementer configures the sub-devices (e.g., inverters, fans, energy storage devices) that require the Edge to access the EnOS Cloud in the EnOS Edge Configuration Center. The sub-devices can be registered using the two methods below:
    - Dynamic Registration: Creates the device to be connected directly in the Edge Configuration Center; the Configuration Center will call the REST API of the IoT Hub to create the device in the EnOS Cloud.
    - Static Registration: Creates the device to be connected in the EnOS Console and then binds it in the Edge Configuration Center. The Edge functions as a proxy and connects the sub-device to the EnOS Cloud.

8. Device Data Transmission
  - The Edge is connected directly to the IoT Hub, and the sub-device is connected to the EnOS IoT Hub via the Edge proxy.
  - The MQTT protocol is used for data transmission between the Edge and the IoT Hub.
  - If the certificate-based two-way authentication is enabled, the data transmission between the Edge and the IoT Hub will be encrypted by the certificate.

#### Scenario 1.2: The connected sub-device is registered, and the device trigraph has been stored in the Edge.

Scenarios 1.1 and 1.2 follow the same basic principles, except that in Scenario 1.1, SA is burned into the Edge and thus allows it to call the EnOS API to create the sub-device. While in Scenario 1.2, you will need to register the sub-device in the cloud beforehand, obtain the sub-device trigraph information, and burn the sub-device trigraph information into the Edge in advance. When configuring the device connection in the Edge Configuration Center, you need to bind the connected device with the pre-burned sub-device trigraph.

Compared with the more flexible Scenario 1.1, Scenario 1.2 has a more complex configuration but with higher security. You may choose Scenario 1.1 if convenience is your priority.

### Direct Connection

![Device connection overview](media/overview_device_connection_2_0_v3_2.png)

#### Scenario 2.1: The connected device is not registered; it is dynamically registered through pluggable information collection.
Take the household photovoltaic inverter for example.

Household photovoltaic inverters do not support burning. In normal scenarios, an acquisition rod is required to collect data and forward them to the cloud. As the acquisition rod only collects data of one inverter, we can consider the inverter and the acquisition rod as one smart device; and since the acquisition rod supports burning, the inverter and the acquisition rod can be regarded as a whole device that supports burning.

1. Create an inverter product in the cloud (under Customer Organization, not Developer Organization).

2. The acquisition rod developer creates an acquisition rod app under Developer OU and obtains the app SA: `accesskey` and `accesssecret`.

3. The acquisition rod developer configures the factory settings of the rod and burns the following credential information into it:
  - SA of the acquisition rod app
  - The `productKey` of the inverter
  - The `orgId` to which `productKey` belongs.

4. The IoT implementer performs on-site construction and installation, installing the acquisition rod on the inverter, powering on the device and connecting it to the network. Once connected, the device will perform the following actions:
  - The acquisition rod collects the serial number of the inverter, and uses it as the `deviceKey`; it then calls the REST API using SA, dynamically creates the device using the `productKey`, `deviceKey` (serial number), and `orgId`, and obtains the device's `deviceSecret`.
  - The acquisition rod records the `deviceSecret`, which will be automatically burned into the firmware of the device.
  - The acquisition rod collects data from the inverter, and uses the `productKey`, `deviceKey`, and `deviceSecret` to connect to the cloud. Once authenticated, the device will go online and send data.



#### Scenario 2.2: The connected device is registered, and the device is burned with its own trigraph before leaving the factory.
This scenario requires the device to be burned with the device trigraph obtained through cloud registration before it leaves the factory. The scenario has higher security but makes burning more difficult and hence has lower operability.


#### Scenario 2.3: The connected device is registered, and the devices are burned with the same product information in batch.
Scenario 2.3 is added to deal with the low operability issue of Scenario 2.2. Which is
1. Devices are burned in batch with the same product certificate (i.e., `productKey` and `productSecret`) before leaving the factory.
2. Device registration can be integrated with the manufacturer's device management system. After each batch of devices is shipped, the customer's device management system can register the devices in batch by calling the REST API.
3. When the devices are sent to the site, powered on, and connected to the network, they can automatically connect to the cloud.
