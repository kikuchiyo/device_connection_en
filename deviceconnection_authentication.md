# Security Authentication Overview

To ensure the security of the devices and data transmission, the device needs to be authenticated before connecting to the EnOS IoT Hub. EnOS supports _Secret-based One-way Authentication_ and _Certificate-based Two-way Authentication_.

## Secret-based Authentication

Before discussing the secret-based one-way authentication mechanism, you need to understand the following concepts:

- **Product credentials**: `ProductKey` and `ProductSecret`.
  - `ProductKey`: Globally unique identifier issued by EnOS for the product.
  - `ProductSecret`: The product secret issued by EnOS, which is paired with `ProductKey`. It's commonly used for dynamic activation of devices. To initiate the dynamic activation, a device first carries `ProductKey`, `ProductSecret` and `DeviceKey` upon its first connection to the EnOS Cloud, to get `DeviceSecret` from the cloud for device activation.
- **Device credentials**: `DeviceKey` and `DeviceSecret`.
  - `DeviceKey`: The device identifier that is automatically generated or defined by the user by the system when a device is being registered. A `DeviceKey` is unique across the OU.
  - `DeviceSecret`: The device secret issued by EnOS, which is paired with `DeviceKey`.
- **Device triple**: Contains three elements, i.e. `ProductKey`, `DeviceKey` and `DeviceSecret`, used for secret-based authentication.

EnOS enforces the secret-based authentication mechanism by default. For more information, see [Secret-based Authentication](secretbased_authentication).

## Certificate-based Two-way Authentication

The secret-based authentication involves device identity authentication through the device triple. It is a one-way authentication mechanism, that is, the IoT Hub validates the identity of the device, however, the device does not verify the identity of the IoT Hub. To enforce two-way authentication, the certificate-based authentication mechanism shall be used.

Before discussing the certificate-based two-way authentication mechanism, you need to understand the following concepts:
- **Certificate Authority (CA)**: A digital certificate issuer that is capable of issuing CA certificates.
- **CA certificate**: A digital certificate whose holder can sign other certificates. It conforms to the certificate format defined by the [IETF RFC 5280](https://tools.ietf.org/html/rfc5280) specification.
- **Device certificates**: The certificates signed and issued by the CA certificate. The device certificates are generated in the following process:
  - A key pair is generated based on the device information.
  - A certificate request file (CSR) is generated based on the key pair.
  - The CSR is sent to the CA.
  - The CA certificate signs and issues the device certificates and registers the device certificates to the CA. Meanwhile, the device certificates are also stored in the device.

EnOS provides CA certificate service, for more information, see [X.509 Certificate Service in EnOS](https://docs.envisioniot.com/docs/enos/en/latest/security/x509_ca/index.html#).

When you enable the certificate-based authentication, you need to use the certificate APIs to generate the device certificates as instructed in [Getting Started with Certificate-Based Authentication](gettingstarted_java_ssl_connection) to establish secure connection between devices and IoT Hub.

When you enable certificate-based two-way authentication, we recommend the following best practices:
- Provide each device with a unique certificate for finer certificate management, such as certificate revocation.
- The device must support replacement of the certificate to streamline to process when the certificate expires.

For details about the certificate-based two-way authentication, see [Certificate-based Two-way Authentication](certificatebased_authentication).
