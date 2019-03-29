# Send Data to EnOS Cloud

When connection is successful, commands can be sent from device to EnOS Cloud. For example, the following code is for login operation of a sub-device in a callback function.  

If network connection is broken for gateway devices, the service will regard all the sub-devices in the topology of the gateway device as offline. While the MQTT client allows automatic re-connection, when the network connection recovers, the `onConnectLost` callback function will be invoked. When the re-connection takes effect, the online logic of the sub-devices will be included in the `onConnectSuccess` callback method.

```java
@Override
public void onConnectSuccess()
{
    try
    {
        System.out.println("start register login sub-device , current status : " + client.isConnected());
        SubDeviceLoginRequest request = SubDeviceLoginRequest.builder().setSubDeviceInfo(subProductKey, subDeviceKey, subDeviceSecret).build();
        SubDeviceLoginResponse rsp = client.publish(request);
        System.out.println(rsp);
    }
    catch (Exception e)
    {
        e.printStackTrace();
    }
}
```

.. note:: Note that the `productKey` of the sub-device should be retrieved from the EnOS Console or through EnOS REST API. The `deviceKey` and `deviceSecret` can also be registered through the `DeviceRegisterRequest` of the SDK.

Now, use the following code sample to send the measurepoint data of a sub-device to the cloud.

```java
public static void postMeasurepoint()
{
      Map<String, String> struct = new HashMap<>();
      struct.put("structKey", "structValue");
      MeasurepointPostRequest request = MeasurepointPostRequest.builder()
                     .setProductKey(subProductKey).setDeviceKey(subDeviceKey)
                     .addMeasurePoint("p1", "string")
                     .addMeasreuPointWithQuality("p2", "value", 2)
                     .addMeasurePoint("p3", 100.2)
                     .addMeasurePoint("p4", struct)
                     .build();
      client.fastPublish(request);
}
```

In this sample, the `fastPublish` method is used. In this way, no response is provided for measurepoints. There are another 2 publish methods in the client.

```java
/**
 * publish the sync request and wait for the response
 * @throws Exception
 */
public <T extends IMqttResponse> T publish(IMqttRequest<T> request) throws Exception

/**
 * publish the request and register the callback , the callback will be called when rcv the response
 * @throws Exception
 */
public <T extends IMqttResponse> void publish(IMqttRequest<T> request, IResponseCallback<T> callback)
```

The difference is that:
- The publish method with callback is asynchronous
- The publish method with response parameters is synchronous. 

Note that if MeasurepointPostRequest calls a push command wongly,  the service does not respond any error messages until session timeout.

The device end provides an API for uploading measurepoint data with quality which you can use to send measurepoint data with quality.
<!--what is the name of this API?-->