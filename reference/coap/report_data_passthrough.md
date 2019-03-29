# 设备发送上行数据

设备可上报原始数据如二进制数据流，设备端会将对应的二进制流发送至EnOS Cloud，EnOS Cloud使用数据脚本解析器将二进制数据流转换成EnOS标准JSON数据格式。

有关如何通过脚本将数据解析为标准格式，参考[创建数据解析脚本](../howto/device/manage/creating_parsing_script)。


- 请求TOPIC：`/sys/${ProductKey}/${DeviceKey}/thing/model/up_raw`

- 响应TOPIC：`/sys/${productKey}/${deviceKey}/thing/model/up_raw_reply`

## 请求数据格式

```
POST /topic/sys/${ProductKey}/${DeviceKey}/thing/model/up_raw

Payload: 设备原始数据如二进制数据
```

## 响应数据格式

```  
Code: <code>               

Payload: <payload>           
```
其中，

- `code`为CoAP返回码，参考[返回码说明](#returncode).
- `payload`为返回数据，如果上行数据处理成功，设备支持的响应数据如二进制数据

### 返回码说明<returncode>

.. csv-table:: 返回码说明
   :header: "Code", "描述", "Payload", "备注"
   :widths: Auto

   "2.04", "Changed", "设备支持的响应数据如二进制数据", "正确请求"
   "4.00", "Bad Request", "无", "请求发送的Payload非法"
   "4.01", "Unauthorized", "无", "未授权的请求"
   "4.03", "Forbidden", "无", "禁止的请求"
   "4.04", "Not Found", "无", "请求的路径不存在"
   "4.05", "Method Not Allowed", "无", "请求方法不合法"
   "5.00", "Internal Server Error", "无", "EnOS Cloud内部错误"
