# 使用DTLS作为安全通道接入设备

## 连接CoAP服务器

服务器地址：xxxx.xxx.xxx.xxxx，端口为5684.

## 建立DTLS安全通道

建立DTLS安全通道时，必须使用Pre-shared Key（PSK）作为密钥交换算法。EnOS
CoAP服务器支持的Cipher Suite有：

-   TLS-PSK-WITH-AES-128-CCM-8

-   TLS-PSK-WITH-AES-128-CBC-SHA256

在DTLS握手的过程中，设备使用的PSK为：

- identity: `\${ProductKey},\${DeviceKey},\${SecureMode},\${Lifetime}`

- key: `SHA-256(\${DeviceSecret})` 中第9到第24字节（共16字节）

PSK中的参数说明如下：

.. csv-table:: 参数说明
   :header: "参数", "说明"
   :widths: Auto

   "ProductKey", "设备三元组中的ProductKey"
   "DeviceKey", "设备三元组中的deviceKey。保证OU下唯一，建议使用NB-IoT模组的IMEI"
   "SecureMode", "2-代表一机一密的认证方式，3-代表一型一密的认证方式"
   "Lifetime", "用于判断设备的在线状态。如果设备在Lifetime内没有与云端发生消息交互，设备会被判断为离线。Lifetime的单位为秒，允许设置30 - 86400内的一个值"
   "DeviceSecret", "设备三元组中的DeviceSecret"
