# Connecting to EnOS Cloud through SSL/TLS

To ensure device security, you can enable the certificate-based authentication so that the device connects to the cloud through SSL/TLS. You can apply device certificate by calling the EnOS certificate service API, load the certificate to the SDK directory, and then connect to the server through the SSL port. The server URL format is `ssl://{regionUrl}:18883`. See the code sample below.

```
client = new MqttClient(betaSSL, productKey, deviceKey, deviceSecret);
client.getProfile().setSSLSecured(true).setSSLJksPath("path.jks", "password");
client.connect(new IConnectCallback() {
    @Override
    public void onConnectSuccess() {
        System.out.println("connect success");
    }

    @Override
    public void onConnectLost() {
        System.out.println("onConnectLost");
    }

    @Override
    public void onConnectFailed(int reasonCode) {
        System.out.println("onConnectFailed : " + reasonCode);
    }
});
```

> You can also use the `setSSLContext()` method to directly set the SSL context, load the certificate content, and complete initializing the MQTT client with certificate-base bi-directional authentication. 
