# Offline Message Integration (Pass-through)

The 3rd-party system may pass raw data (such as binary data) through to EnOS. Raw data includes measure points, attributes and events. EnOS will convert the raw data into corresponding standard data formats by using the data-parsing script that users have defined. Data passed through has no common message body.


Upstream
- Request TOPIC: `sys/${productKey}/integration/up_raw`

- Response TOPIC：`sys/${productKey}/integration/up_raw_reply`

For more information about configuring data parsing scripts, see [Creating Data Parsing Scripts] (../../../../howto/device/manage/creating_data_parsing_script).
