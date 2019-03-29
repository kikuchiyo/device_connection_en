## 调用设备服务

应用可以通过EnOS开放的API调用设备服务。具体参考：（调用服务相关的API接口文档）

EnOS Cloud会根据用户提交的脚本将标准数据格式的服务调用请求，转换成相应的原始数据格式如二进制流。EnOS Cloud会缓存这个二进制流，待设备发送上行数据时，在响应消息内通知设备。

如果当前有缓存的设备服务调用，设备在发送上行数据后，EnOS Cloud会在响应中返回平台定义的Option（2100）。

## 云端返回Option

```
Code: 上行数据返回码

Payload: 上行数据响应Payload

Customized Option 2100:
/topic/sys/${ProductKey}/${DeviceKey}/thing/model/down_raw

```

.. csv-table:: 参数说明
   :header: "参数", "说明"
   :widths: Auto

   "ProductKey", "设备三元组中的ProductKey"
   "DeviceKey", "设备三元组中的deviceKey。保证OU下唯一，建议使用NB-IoT模组的IMEI"

## 设备端调用服务

设备在收到这个Option后，可以通过服务调用请求，获取服务调用。

请求格式： `GET /topic/sys/${ProductKey}/${DeviceKey}/thing/model/down_raw`


如果有更多的服务调用

```
Code: CoAP返回码，参考Code说明

Payload: 如果服务调用查询处理成功，设备支持的服务调用数据如二进制数据

Customized Option 2100:
/topic/sys/\${ProductKey}/\${DeviceKey}/thing/model/down_raw
```

如果有多个服务调用，设备可以重复这个服务调用查询过程。
