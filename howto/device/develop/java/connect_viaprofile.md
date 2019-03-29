# Using Connection Profile File to Connect to EnOS Cloud

除了使用动态代码的方式连接至服务器，SDK还提供了配置文件的方式进行连接，用户只需要提前配置一下的配置文件，提供必要的参数信息

```java
//store config by mqtt sdk
//Mon Jan 14 20:39:20 CST 2019
{
  "serverUrl": "tcp://10.27.21.6:11883", //mandatory
  "productKey": "fKInRgVP", //mandatory
  "deviceKey": "zscai_test_activate",//mandatory
  "productSecret": "c3PW03srd6c",//needed when login by securemode=3
  "deviceSecret":"", //needed when login by securemode=2
  "operationTimeout": 60,//timeout seconds of each operation
  "keepAlive": 60,//conneciton keepAlive  seconds
  "connectionTimeout": 30, //connect timeout seconds
  "maxInFlight": 10000, //maxInFlight mqtt requests
  "autoReconnect": true,//auto reconnect the mqtt client when connect lost
  "sslSecured":false,//enable the ssl connection
  "sslAlgorithm": "SunX509",//ssl algorithm
  "sslJksPath": "",//path of jks file
  "sslPassword": "",//password of jks file
  "subDevices": //if subDevies is config, subdevice will auto login by sdk when mqtt connection build 
   [
    {
      "productKey": "subProduct",
      "deviceKey": "subdevice",
      "deviceSecret": "xxx"
    },
    {
      "productKey": "subProduct",
      "deviceKey": "subdevice",
      "deviceSecret": "xxx"
    }
  ]
}
```
其中regionURL,productKey,deviceKey是必填参数，deviceSecret和productSecret必须提供一个参数，用于完成必要的参数签名校验。
当配置文件中提供了参数deviceSecret则采用securemode=2进行登录，如果没有提供deviceSecret，而提供了productSecret那么采用securemode=3进行登录。
用于可以使用如下的代码，使用配置文件的方式完成连接过程。
 
需要注意的是如果在配置文件中配置了子设备信息，那么SDK会在连接成功之后，自动登录子设备，*这些子设备需要在云端预先配置成该网关设备的子设备*。如果用户需要手动的管理子设备的状态，那么可以不将子设备配置在配置文件中，用户根据SubDeviceLoginRequest手动的管理子设备的上线。
同样的如果子设备登录方式使用securemode=3动态激活方式登录，那么云端会返回设备对应的设备密钥至设备端，设备端需要持久化保存该设备密钥信息，后续使用设备密钥进行登录签名认证。同样的java sdk已经封装了这一过程。

使用配置文件方式连接服务的示例代码如下：

```java
    public void connect() {
        MqttClient client = new MqttClient(new FileProfile(".config"));
        System.out.println("start connect with callback ... ");
        try {
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
        } catch (EnvisionException e) {
            //e.printStackTrace();
        }
        System.out.println("connect result :" + client.isConnected());
    }
```