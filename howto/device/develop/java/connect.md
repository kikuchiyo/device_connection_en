# Connecting to EnOS Cloud

Use the following code to connect the device to EnOS Cloud.

In the following sample:
- `serverUrl` is the address of the server. If using TCP connection, the format of the server URL can be `tcp://{regionUrl}:11883`. 
- The <`productKey`, `deviceKey`,`deviceSecret`> (or <`productKey`, `deviceKey`,  `productSecret`> when the device is to be dynamically activated) are the device credentials issued by EnOS when you register the device. For more information about device registeration, see [Connecting Smart Device into EnOS Cloud](/docs/device-connection/en/latest/quickstart/gettingstarted_device_connection).


```java
MqttClient client = new MqttClient(serverUrl, productKey, deviceKey, deviceSecret);
client.connect(new IConnectCallback()
{
	@Override
	public void onConnectSuccess()
	{
		System.out.println("onConnectSuccess");
	}

	@Override
	 public void onConnectLost()
	{
		System.out.println("onConnectLost");
	}

	@Override
	public void onConnectFailed(int reasonCode)
	{
		System.out.println("onConnectFailed");
	}
});
```

