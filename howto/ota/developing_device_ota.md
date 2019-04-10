# Developing OTA Capabilities on Devices

## About This Task

The device end OTA upgrade largely depends on the physical space and function implementation of the device itself. The EnOS platform provides a device SDK that includes OTA capabilities for hardware developers, which supports the following capabilities:

- Device escalates the firmware version information: The device escalates its version information once when it connects to the cloud, and the cloud records the device's version number;
- Device receives the upgrade request pushed by the cloud: The device receives the upgrade request pushed by the cloud and downloads the firmware file;
- Device requests actively the upgradeable firmware version: It is supported for the device to request and query any upgradeable version information to the cloud;
- Device escalates the upgrade progress and the reasons for upgrade failure: The device may escalate its upgrade progress or the reasons for upgrade failure during its upgrade process for O&M personnel to perform remote upgrade management;

.. note:: Generally, the device OTA upgrade requires necessary physical conditions. The EnOS platform provides the cloud message channels and file download services for device OTA upgrade, and provides a device end SDK for developers to call the interfaces. The real device end firmware upgrade relies on the ability of device end Flash to provide sufficient physical space, while the developers should implement the business logics like firmware switching, booting and restart after the firmware file is download.


### Firmware upgrade TOPIC

The EnOS Cloud provides the message topics for firmware upgrade, and the upgrade request supports MQTT-based message sending and subscription:

1. The device end escalates its firmware version to the cloud: The device issues the permissions to escalate its current firmware version information after it connects to the cloud successfully

   Request topic: `/sys/${productkey}/${devicekey}/ota/device/inform`

   Response topic: `/sys/${productkey}/${devicekey}/ota/device/inform_reply`

2. The device end receives the OTA request from the cloud: The device end subscribes the permissions to receive the OTA upgrade notifications pushed by the cloud, including firmware name, version number, MD5 and download URL.

   Request topic: `/sys/${productkey}/${devicekey}/ota/device/upgrade`

   Response topic:  `/sys/${productkey}/${devicekey}/ota/device/upgrade_reply`

3. The device end escalates its firmware upgrade progress: The device requests the firmware download through HTTPS cycle, and escalates the firmware upgrade event, error code and download progress (%) through this topic

   Request topic: `/sys/${productkey}/${devicekey}/ota/device/progress`

   Response topic: ` /sys/${productkey}/${devicekey}/ota/device/progress_reply`

4. The device requests actively the upgradeable firmware versions: The cloud creates an OTA upgrade policy as "Upon device request", and the device may issue the upgrade request through this topic and receives the available version information returned from the cloud.

   Request topic: `/sys/${productkey}/${devicekey}/ota/device/getversion`

   Response topic:  `/sys/${productkey}/${devicekey}/ota/device/getversion_reply`


## Before You Start

- You have understood the OTA upgrade process in EnOS. See [Overview of Device Firmware Upgrade](ota_overview).

## Step 1: Installing Device SDK

Download [enos-mqtt-sdk-java](https://github.com/EnvisionIot/enos-mqtt-sdk-java)。 If Maven is sued, its dependencies are given as follows:

```
<dependency>
  <groupId>com.envisioniot</groupId>
  <artifactId>enos-mqtt</artifactId>
  <version>2.1.2</version>
</dependency>
```

## Step 2: Downloading device firmware

   - Download the file by using the REST API `getFile`. You may view the API documentation by clicking **EnOS API > API Documentation > Common File Service > getFile** in the navigation bar in the EnOS Console.

   - Through cloud service SDK
     - [Java SDK](https://github.com/EnvisionIot/enos-api-sdk-java)
     - [python SDK](https://github.com/EnvisionIot/enos-api-sdk-python)

## Sample codes

The below is the sample codes for developing the device end OTA capabilities by using Java SDK:

```java
import com.envisioniot.enos.iot_mqtt_sdk.core.IConnectCallback;
import com.envisioniot.enos.iot_mqtt_sdk.core.MqttClient;
import com.envisioniot.enos.iot_mqtt_sdk.core.exception.EnvisionException;
import com.envisioniot.enos.iot_mqtt_sdk.core.msg.IMessageHandler;
import com.envisioniot.enos.iot_mqtt_sdk.core.msg.IMqttDeliveryMessage;
import com.envisioniot.enos.iot_mqtt_sdk.core.profile.DefaultProfile;
import com.envisioniot.enos.iot_mqtt_sdk.message.downstream.ota.OtaUpgradeCommand;
import com.envisioniot.enos.iot_mqtt_sdk.message.upstream.ota.*;

import java.util.List;
import java.util.concurrent.TimeUnit;

/**
 * device firmware over-the-air
 */
public class OtaSample {

    //Please use your own productKey, deviceKey, and deviceSecret
    static String productKey = "testPK";
    static String deviceKey = "testDK";
    static String deviceSecret = "testDS";

    //Use the actual mqtt-broker url
    static String brokerUrl = "tcp://{mqtt-broker-url}";

    static MqttClient client;

    public static void main(String[] args) throws Exception {
        client = new MqttClient(new DefaultProfile(brokerUrl, productKey, deviceKey, deviceSecret));
        initWithCallback(client);

        //Report firmware version first
        reportVersion("initVersion");

        //        upgradeFirmwareByCloudPush();


        //        upgradeFirmwareByDeviceReq();
    }

    public static void upgradeFirmwareByCloudPush() {
        client.setArrivedMsgHandler(OtaUpgradeCommand.class, new IMessageHandler<OtaUpgradeCommand, IMqttDeliveryMessage>() {
            @Override
            public IMqttDeliveryMessage onMessage(OtaUpgradeCommand otaUpgradeCommand, List<String> list) throws Exception {
                System.out.println("receive command: " + otaUpgradeCommand);

                Firmware firmware = otaUpgradeCommand.getFirmwareInfo();

                //TODO: download firmware from firmware.fileUrl

                //Mock reporting progress
                reportUpgradeProgress("20", "20");
                TimeUnit.SECONDS.sleep(2);

                reportUpgradeProgress("25", "25");
                TimeUnit.SECONDS.sleep(20);

                reportUpgradeProgress("80", "80");
                TimeUnit.SECONDS.sleep(20);

                //Firmware upgrade success, report new version
                reportVersion(otaUpgradeCommand.getFirmwareInfo().version);

                return null;
            }
        });
    }

    public static void upgradeFirmwareByDeviceReq() throws Exception {
        List<Firmware> firmwareList = getFirmwaresFromCloud();
        String version = null;
        for (Firmware firmware : firmwareList) {
            version = firmware.version;
            StringBuffer sb = new StringBuffer();
            sb.append("Firmware=>[");
            sb.append("version=" + firmware.version);
            sb.append("signMethod=" + firmware.signMethod);
            sb.append("sign=" + firmware.sign);
            sb.append("fileUrl=" + firmware.fileUrl);
            sb.append("fileSize=" + firmware.fileSize);
            sb.append("]");
            System.out.println(sb.toString());
        }
        if (version != null) {
            reportUpgradeProgress("20", "20");
            TimeUnit.SECONDS.sleep(10);
            reportUpgradeProgress("80", "80");
            TimeUnit.SECONDS.sleep(20);
            reportVersion(version);
        }
    }

    public static void reportVersion(String version) throws Exception {
        OtaVersionReportRequest.Builder builder = new OtaVersionReportRequest.Builder();
        builder.setProductKey(productKey).setDeviceKey(deviceKey).setVersion(version);
        OtaVersionReportRequest request = builder.build();
        System.out.println("send =>" + request.toString());
        client.fastPublish(builder.build());
    }

    private static void reportUpgradeProgress(String progress, String desc) throws Exception {
        OtaProgressReportRequest.Builder builder = new OtaProgressReportRequest.Builder();
        builder.setStep(progress).setDesc(desc);
        client.fastPublish(builder.build());
    }

    private static List<Firmware> getFirmwaresFromCloud() throws Exception {
        OtaGetVersionRequest.Builder builder = new OtaGetVersionRequest.Builder();
        builder.setProductKey(productKey).setDeviceKey(deviceKey);
        OtaGetVersionRequest request = builder.build();
        OtaGetVersionResponse response = client.publish(request);
        System.out.println("send getversion request =>" + request.toString());
        System.out.println("receive getversion response =>" + response.toString());
        return response.getFirmwareList();
    }

    private static void initWithCallback(MqttClient client) {
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
            e.printStackTrace();
        }
    }
}
```

## Firmware upgrade protocol

### Reporting Version Number

The device may send its current firmware version number to EnOS, and only the device that has escalated its firmware version number can create the upgrade task in the console.

Uplink TOPIC

- Request topic: `/sys/${productkey}/${devicekey}/ota/device/inform`
- Response topic: `/sys/${productkey}/${devicekey}/ota/device/inform_reply`

Request data format:

```JSON
{
    "id":"123",
    "version":"1.0",
    "method":"ota.device.inform",
    "params": {
        "version":"xxxxxxxx"
    }
}
```

Response data format:

```JSON
{
    "id": "123",
    "code": 200,
    "data": {}
}
```

Parameter descriptions:

.. list-table::
   :widths: auto

   * - Parameters
     - Type
     - Necessary or not
     - Description
   * - id
     - Long
     - Optional
     - Message ID (retention value)
   * - version
     - String
     - Required
     - Protocol version, which is V1.0 now
   * - method
     - String
     - Required
     - Request method, which must be ota.device.inform
   * - params
     - Object
     - Required
     - Escalate version number
   * - version
     - String
     - Required
     - Escalated version number
   * - code
     - Integer
     - Required
     - Result return code, where 200 means that the request is executed successfully

### Receiving Upgrade Request From EnOS

After the firmware upgrade task is created in the console, the qualified online devices will receive the firmware information pushed from the cloud, and the offline devices will receive the upgrade request after backing online next time.

Downlink TOPIC:

- Request topic: `/sys/${productkey}/${devicekey}/ota/device/upgrade`
- Response:  `/sys/${productkey}/${devicekey}/ota/device/upgrade_reply`

Request data format:
```JSON
{
    "id":"123",
    "version":"1.0",
    "method":"ota.device.upgrade",
    "params": {
        "version":"v1.0",
        "sign":"xxxxxxx",
        "signMethod":"md5",
        "fileUrl":"/1b30e0ea83002000/ota/kadak13",
        "fileSize":1024
    }
}
```

Response data format:
```JSON
{
    "id": "123",
    "code": 200,
    "data": {}
}
```

Parameter descriptions:

.. list-table::
   :widths: auto

   * - Parameters
     - Type
     - Necessary or not
     - Description
   * - id
     - Long
     - Optional
     - Message ID (retention value)
   * - version
     - String
     - Required
     - Protocol version, which is V1.0 now
   * - method
     - String
     - Required
     - Request method, which must be ota.device.getversion
   * - params
     - Object
     - Optional
     - None
   * - code
     - Integer
     - Required
     - Result return code, where 200 means that the request is executed successfully
   * - data
     - List
     - Optional
     - Returned detailed information in JSON format
   * - version
     - String
     - Required
     - Firmware version number
   * - sign
     - String
     - Required
     - Firmware signature
   * - signMethod
     - String
     - Required
     - Firmware signature algorithm
   * - fileUrl
     - String
     - Required
     - Firmware file url
   * - fileSize
     - Long
     - Required
     - Firmware file size in bytes

### Reporting Upgrade Progress

After the device starts to download the firmware, it may escalate its upgrade progress or reasons for upgrade errors through this topic, and the O&M personnel may view the upgrade progress in the console.

Uplink TOPIC:
- Request topic: `/sys/${productkey}/${devicekey}/ota/device/progress`
- Response topic: `/sys/${productkey}/${devicekey}/ota/device/progress_reply`

Request data format:
```JSON
{
    "id":"123",
    "version":"1.0",
    "method":"ota.device.progress",
    "params": {
        "step":"1",
        "desc":"xxxxxxxx"
    }
}
```

Response data format:
```JSON
{
    "id": "123",
    "code": 200,
    "data": {}
}
```

Parameter descriptions:

.. list-table::
   :widths: auto

   * - Parameters
     - Type
     - Necessary or not
     - Description
   * - id
     - Long
     - Optional
     - Message ID (retention value)
   * - version
     - String
     - Required
     - Protocol version, which is V1.0 now
   * - method
     - String
     - Required
     - Request method, which must be ota.device.process
   * - params
     - Object
     - Required
     - Escalate progress parameter
   * - step
     - String
     - Required
     - Escalated firmware upgrade progress ratio; its normal range is [0, 100], where -1 refers to upgrade failure; -2 refers to download failure; -3 refers to verification failure; -4 refers to burning failure
   * - desc
     - String
     - Optional
     - Description for current step, which may carry error information in case of any exception
   * - code
     - Integer
     - Required
     - Result return code, where 200 means that the request is executed successfully


### Requesting Upgrade

In case of non-forced upgrade, the upgrade task for device to request actively upgrade may be created in the console; at this point, the cloud will not actively push any upgrade request but wait until the device requests actively upgrade to obtain upgradeable version information; if there are multiple versions available in the cloud, a list of upgradeable versions will be returned and the device or its owner may select a proper one from it for upgrade purpose.


Uplink TOPIC

- Request topic: `/sys/${productkey}/${devicekey}/ota/device/getversion`
- Response topic:  `/sys/${productkey}/${devicekey}/ota/device/getversion_reply`

Request data format

```JSON
{
    "id":"123",
    "version":"1.0",
    "method":"ota.device.getversion",
    "params": {
    }
}
```

Response data format:

```JSON
{
    "id":"123",
    "code":200,
    "data": [
         {
            "version":"v1.0",
            "sign":"xxxxxxx",
            "signMethod":"md5",
            "fileUrl":"/1b30e0ea83002000/ota/kadak13",
            "fileSize":1024
        }
    ]
}
```


Parameter descriptions:

.. list-table::
   :widths: auto

   * - Parameters
     - Type
     - Necessary or not
     - Description
   * - id
     - Long
     - Optional
     - Message ID (retention value)
   * - version
     - String
     - Required
     - Protocol version, which is V1.0 now
   * - method
     - String
     - Required
     - Request method, which must be ota.device.getversion
   * - params
     - Object
     - Optional
     - None
   * - code
     - Integer
     - Required
     - Result return code, where 200 means that the request is executed successfully
   * - data
     - List
     - Optional
     -  Returned detailed information in JSON format; if there are multiple upgradeable versions for this device in the cloud, the information for multiple versions will be returned
   * - version
     - String
     - Required
     - Firmware version number
   * - sign
     - String
     - Required
     - Firmware signature
   * - signMethod
     - String
     - Required
     - Firmware signature algorithm
   * - fileUrl
     - String
     - Required
     - Firmware signature algorithm
   * - fileSize
     - Long
     - Required
     - Firmware file size in bytes


### Exceptions

The exceptions that occur during the firmware upgrade may be represented by using the parameters step and desc when escalating the firmware upgrade progress. The parameter value of step is less than 0, it indicate an exception, and the parameter desc refers to the descriptions of exception.

The parameter step for exceptions provided by the current system is shown as follows:

.. list-table::
   :widths: auto

   * - step value
     - Meaning
   * - -1
     - Upgrade failure
   * - -2
     - Download failure
   * - -3
     - Verification failure
   * - -4
     - Burning failure

In case of other custom exceptions, you may set step as a number less than -4, and set desc as the description of corresponding exception.
