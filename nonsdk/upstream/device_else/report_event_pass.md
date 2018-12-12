# Report Device Events​ (Passthrough)

If passthrough mode is used, the device sends raw data such as a binary data stream to the cloud. EnOS Cloud converts the raw data to JSON format using the script that you defined. The raw data can be of any format. For more information about the request and response format, see [Report Device Events​ (non-passthrough)](report_event_nopass).

Upstream
- Request TOPIC: `/sys/{productKey}/{deviceKey}/thing/model/up_raw`

- Reply TOPIC：`/sys/{productKey}/{deviceKey}/thing/model/up_raw_reply`
