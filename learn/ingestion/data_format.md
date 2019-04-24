# Data Format

The devices transmit data to the cloud as per the attributes, measurepoints, events and services defined in the model. EnOS supports the data in EnOS standard JSON format and custom format.

## EnOS standard data format

In general, we recommend to transmit data in EnOS standard JSON format.

The sample codes below show the standard data format used for uploading data into the cloud:

```json
{
        "id": "123",
        "version": "1.0",
        "params": {
                "measurepoints": {
                        "Power": {
                                "value": 1.0,
                                "quality": 9
                        },
                        "temp": 1.02,
                        "branchCurr": [
                                "1.02", "2.02", "7.93"
                        ]
                },
                "time": 123456
        },
        "method": "thing.measurepoint.post"
}
```

The sample codes below show the standard data format used for issuing data from the cloud to devices:

```json
{
        "id": "123",
        "version": "1.0",
        "params": {
                "temperature": 30.5
        },
        "method": "thing.service.measurepoint.set"
}
```

In the above-mentioned sample codes:

- `id` refers to the message ID
- `version` refers to the protocol version
- the JSON arrays packaged by `params` refer to the data to be transmitted
- `method` refers to the request method

The EnOS device protocol defines in which format and by which topic the device transmits the data to the cloud. For more information, see [Device Protocol](../../reference/mqtt/index).

## Custom data format

The JSON format-based data communication with the cloud is not suitable for the devices with lower configuration and limited resources or that have special requirements on networking traffic. In this scenario, you can pass through the data to the cloud, and then the cloud runs the parsing scripts to convert the data into the JSON format defined by EnOS.  When the cloud sends the control commands to the device, the scripts may also be used to convert the JSON format defined by EnOS into the binary data that the device is able to parse for issuing purpose.

For the devices that transmit the data by means of pass-through or in the custom format, you may compile scripts in the EnOS Cloud to parse the data from devices. The parsing scripts support JavaScript-based development.

EnOS parser provides the following capabilities:

1. Editing script online, support the validation of JavaScript syntax.

2. Upstream & downstream messaging simulation and debugging, support the viewing of simulation result.

3. Runtime environment after the publishing of script can be invoked for upstream & downstream messaging.

For more information, see [Creating Data Parsing Script](../../howto/device/manage/creating_data_parsing_script).
