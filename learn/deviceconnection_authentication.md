# Device and Cloud Security

To ensure the security of the devices and data transmission, the device needs to be authenticated before connecting to the EnOS IoT Hub. EnOS supports _Secret-based One-way Authentication_ and _Certificate-based Two-way Authentication_.

## Secret-based Authentication

Secret-based authentication refers to the authentication of devices based on device triple, i.e. `ProductKey`, `DeviceKey` and `DeviceSecret`.

Before discussing the secret-based authentication mechanism, you need to understand the following concepts:

- **Product key-secret pair**: `ProductKey` and `ProductSecret`.

  - `ProductKey`: Globally unique identifier issued by EnOS for the product.
  - `ProductSecret`: The product secret issued by EnOS, which is paired with `ProductKey`. It's commonly used for dynamic activation of devices. To initiate the dynamic activation, a device first carries `ProductKey`, `ProductSecret` and `DeviceKey` upon its first connection to the EnOS Cloud, to get `DeviceSecret` from the cloud for device activation.

- **Device key-secret pair**: `DeviceKey` and `DeviceSecret`.

  - `DeviceKey`: The device identifier that is automatically generated or defined by the user by the system when a device is being registered. A `DeviceKey` is unique across the OU.
  - `DeviceSecret`: The device secret issued by EnOS, which is paired with `DeviceKey`.

- **Device triple**: Contains three elements, i.e. `ProductKey`, `DeviceKey` and `DeviceSecret`, used for secret-based authentication.

### Device State Transition Phases

The following operations and states are involved in the connection between the device and the EnOS IoT Hub:

- **Registration**
  A device instance is created in the cloud through the web-based EnOS Console or by calling the REST API.

- **Login**
  The device must be successfully logged in before it can send data. The device triple authentication is required for login.

- **Activation**
  The device will be activated upon its first successful login, which updates its status from **Inactive** to **Active**. The **Active** status contains two sub-statuses: **Online** and **Offline**.

### Device Activation Mode and Device States

Devices created for the first time on the EnOS platform are enabled but not activated by default; they are waiting to be activated. Devices can be activated in the _dynamic_ or _static_ mode.

- **Dynamic Activation**: The process of dynamic activation is as follows:

  1. When trying to connect for the first time, the device will carry the `ProductKey`, `ProductSecret`, and `DeviceKey` to request for activation. If the authentication is successful, a `DeviceSecret` will be returned to the device.

  2. The device tries to log in using the `ProductKey`, `DeviceKey`, and `DeviceSecret`.

  3. Once the device successfully logs in, its status will change from **Inactive** to **Online**. The device will then be able to send telemetry. If no telemetry is sent within a certain period of time, the status of the device will change to **Offline**.

  To use dynamic activation, you will need to enable **Dynamic Activation** in the product configuration.

- **Static Activation**: The process of static activation is as follows:

  1. The device sends a login request carrying the `ProductKey`, `DeviceKey`, and `DeviceSecret`.

  2. Once the device is successfully logged in, its status will change from **Inactive** to **Online**. The device will now be able to send data. If no data is sent within a certain period of time, the status of the device will change to **Offline**.

When the device is not working properly or you do not want to receive its data, you can set it to **Disabled**, after which the device will automatically go offline and its status will change to **Offline**.

Three dimensions are used to describe the overall state of the device: Operational State, Activation State, and Communication State, as shown in the following table:

.. list-table::
   :widths: auto

   * - Operational State
     - Activation State
     - Communication State
   * - Disable
     - \
     - Offline
   * - Enable
     - Inactive
     - \
   * - \
     - Activated
     - Online
   * - \
     - \
     - Offline

### Authentication Process

The main authentication process for device connection is as follows:

1. Pre-register device in the cloud.

2. On the edge side, configure the device information registered in the cloud, and mainly burn into the device triple.

3. Power-on on edge side, connect to network, and try to log in. Device triple authentication in the cloud.

   - Successful: Returned successfully, the device is instructed to send data
   - Failure: Return failed, connection is interrupted

4. The device sends data via MQTT protocol.

5. The cloud issues instructions via the MQTT protocol.

6. The device side responds to the cloud requests

The specific flow chart is as follows:

.. image:: ../media/secret_communication.png

## Certificate-based Authentication

The secret-based authentication involves device identity authentication through the device triple. It is a one-way authentication mechanism, that is, the IoT Hub validates the identity of the device, however, the device does not verify the identity of the IoT Hub. To enforce two-way authentication, the certificate-based authentication mechanism shall be used.

When certificate authentication is enabled in the product configuration，EnOS enforces the following security schemes to secure the connection between the EnOS Edge and EnOS IoT Hub:

- The communications between the EnOS Edge and EnOS IoT Hub are enforced to use certificate-based bi-directional authentication.
- Support for RSA algorithm to verify signature, with enforcement for 2048 bits.

Before discussing the certificate-based two-way authentication mechanism, you need to understand the following concepts:

- **Certificate Authority (CA)**: A digital certificate issuer that is capable of issuing CA certificates.
- **CA certificate**: A digital certificate whose holder can sign other certificates. It conforms to the certificate format defined by the [IETF RFC 5280](https://tools.ietf.org/html/rfc5280) specification.
- **Device certificates**: The certificates signed and issued by the CA certificate. The device certificates are generated in the following process:

  - A key pair is generated based on the device information.
  - A certificate request file (CSR) is generated based on the key pair.
  - The CSR is sent to the CA.
  - The CA certificate signs and issues the device certificates and registers the device certificates to the CA. Meanwhile, the device certificates are also stored in the device.

### Authentication Process

#### Setup Phase

The following diagram illustrates the process of secure communication between the edge and IoT Hub based on X.509 certificates:

**1. IoT Hub Acquires X.509 Certificate**

.. image:: ../media/certificate_service_secure_communication_01.png

1a. The IoT Hub creates key pairs and CSR locally, acquires the X.509 certificate with the CSR by using the X.509 Certificate Service API.

1b. The EnOS CA issues the X.509 certificate and sends the certificate to the IoT Hub.

1c. The IoT Hub receives and stores the X.509 certificate.

**2. Edge Acquires X.509 Certificate**

.. image:: ../media/certificate_service_secure_communication_02.png

2a. Before leaving the factory, the Edge devices are pre-burned with a product certificate (`ProductKey` and `ProductSecret`) as well as a device serial number (SN). When powered on and connected to the network, the device will report its product certificate and serial number to the cloud for dynamic activation. The cloud will return the `DeviceSecret` to the Edge if the authentication is successful.

2b. On the IoT Hub, the serial number of the Edge device is used as the `DeviceKey` to pre-register the Edge device. The device can be registered either via the EnOS Console or by calling the REST API.

2c. The Edge receives the responses from the IoT Hub, creates key pairs and CSR, and calls the API to get its X.509 certificate. Meanwhile, the device trigraph is used to log the device in to the cloud, and the device will be activated upon its first login.

2d. The IoT Hub receives the CSR from the edge, after verifying its identity, forward the CSR to the EnOS CA.

2e. The EnOS CA receives the CSR, issues the edge certificate and responds to the IoT Hub.

2f. The IoT Hub receives the issued X.509 certificate, binds it with the device id, and then sends the edge certificate to the edge.

2g. The edge receives the edge certificate, saves them securely in the local repository, for example, the Trusted Platform Module (TPM).

#### Communication Phase

The diagram below illustrates the certificate-based authentication process:

**3. Edge Communicates with the IoT Hub through Certificate-based Bi-directional Authentication**

.. image:: ../media/certificate_service_secure_communication_03.png

3a. The edge validates the certificate of the IoT Hub.

3b. The IoT Hub validates the certificate of the edge.

When the TLS handshake in step 3a and 3b succeeds, the TLS connection is established between the edge and the IoT Hub.

3c. The edge transmits device telemetry through MQTT over the TLS connection.

3d. The IoT Hub transmits configurations and control signals through MQTT over the TLS connection.

#### Revocation Phase

Under some circumstances, user needs to revoke the X.509 certificate of the edge. The following diagram illustrates the revocation process.

**4. The IoT Hub Revokes the X.509 Certificate of the Edge**

.. image:: ../media/certificate_service_secure_communication_04.png

4a. The IoT Hub calls the revocation API to revoke the X.509 certificate with the serial number of the certificate.

4b. The EnOS CA receives the request from the IoT Hub, verifies the identity, revokes the certificate, and updates the CRL.

### Edge Security Best Practices

In the certificate-based security connection, consider the following best practices to secure the edge:

- Create the private key for the edge and keep it secret in a storage such as TPM.
- Use TLS 1.2 when communicating with the IoT Hub, and verify that the server certificate is valid.
- Each edge must have a unique public/private key pair.
- The key pair used to be authenticated by IoT Hub should not be used for other purposes or communications through other protocols.
- The key must be revoked when the edge is reset.
- When your edge runs on an operating system, make sure your operating system is secured through certain mechanisms, for example, firewall.
- Ensure that you have a way to update root CA certificates and CRL.
- Ensure that the clock on the edge is not tampered with.

When you enable certificate-based two-way authentication, we recommend the following best practices:

- Provide each device with a unique certificate for finer certificate management, such as certificate revocation.
- The device must support replacement of the certificate to streamline to process when the certificate expires.

## Next Steps

EnOS enforces the secret-based authentication mechanism by default. The keys and secrets are generated or specified when you [Creating a Product](../howto/device/manage/creating_product) and [Creating a Device](../howto/device/manage/creating_device).

When you enable the certificate-based authentication, you need to use the certificate APIs to generate the device certificates as instructed in [Getting Started with Certificate-Based Authentication](../quickstart/gettingstarted_java_ssl_connection) to establish secure connection between devices and IoT Hub.
