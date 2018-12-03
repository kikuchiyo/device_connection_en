# Report Device Events​ (passthrough)

If passthrough mode is used, the device sends raw data such as a binary
data stream to EnOS cloud. EnOS Cloud convert the raw data to JSON
format by the script you have submitted to the EnOS. The raw data can be
in any format.For more information about the request and response format
, refer to Report device events​ (non-passthrough).

Upstream
- Request TOPIC: /sys/{productKey}/{deviceKey}/thing/model/up_raw

- Reply TOPIC：/sys/{productKey}/{deviceKey}/thing/model/up_raw_reply
