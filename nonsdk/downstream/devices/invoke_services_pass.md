# Invoke Device Services (Passthrough）

If passthrough mode is used, the device sends raw data such as a binary data stream to EnOS Cloud.

For more information about the format of request and response, see [Invoke Device Services (Non-Passthrough)](invoke_services_nopass).

Downstream
- Request TOPIC: `/sys/{productKey}/{deviceKey}/thing/service/down_raw`

- Reply TOPIC: `/sys/{productKey}/{deviceKey}/thing/service/down_raw_reply`
