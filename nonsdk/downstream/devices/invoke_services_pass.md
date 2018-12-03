# Invoke Device Services (passthrough）

If passthrough mode is used, the device sends raw data such as a binary data stream to EnOS Cloud.

For more information about the request and response format, refer to
Invoke device services (non-passthrough).

Downstream
- Request TOPIC /sys/{productKey}/{deviceKey}/thing/service/down_raw

- Reply TOPIC /sys/{productKey}/{deviceKey}/thing/service/down_raw_reply
