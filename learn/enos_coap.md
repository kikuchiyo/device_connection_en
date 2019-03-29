# 基于CoAP协议的连接

CoAP协议适用在资源受限的低功耗设备上，尤其是NB-IoT的设备使用。

## EnOS CoAP协议标准

支持基于UDP的RFC 7252 CoAP协议，具体请参考：[RFC 7252](https://tools.ietf.org/html/rfc7252)

- EnOS CoAP接入支持可确认请求（CON），响应会以Piggybacked形式在ACK消息中返回。

- EnOS CoAP接入实现了RFC 7252协议规定的CoAP缓存功能，因此要求设备对于每一个新的请求，使用不同CoAP Message ID和Token。

- 目前必须使用DTLS v1.2保证通道安全，具体请参考：[RFC 6347](https://tools.ietf.org/html/rfc6347)

- 支持CoAP协议中的Block-wise传输功能，具体参考：[RFC 7959](https://tools.ietf.org/html/rfc7959)

- EnOS CoAP接入目前不支持资源发现功能，不支持资源观察功能。

- 通过CoAP传输数据的大小依赖于MTU的大小，建议在1KB以内。

## 马上开始

1.  在EnOS控制台注册设备并获取设备三元组（`ProductKey`，`DeviceKey`和`DeviceSecret`）并烧录到设备中，建议使用NB-IoT模组的IMEI作为`DeviceKey`。参考[将智能设备连接至EnOS Cloud](../quickstart/gettingstarted_device_connection)。

2.  在设备端集成EnOS CoAP设备协议。

3.  将NB-IoT设备通过运营商的蜂窝网络连接入网。

4.  设备开发者可以通过CoAP/DTLS协议，将设备采集的实时数据上报到EnOS Cloud，借助EnOS，实现设备的安全连接和数据管理能力。参考[基于CoAP的设备端协议](../reference/coap/index).

5.  通过EnOS提供的数据开放接口和消息订阅推送服务，将数据转发到应用服务中，实现资产与应用的快速集成。


