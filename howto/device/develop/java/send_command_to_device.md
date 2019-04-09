# Send Command to Device

The following section introduces how to handle the downstream commands sent from EnOS cloud to device. On the device end, response messages can be configured in the `onMessage` callback function, so that the SDK can respond the messages to the cloud. You can configure the error codes and error messages to indicate failure of commands to the device. You can choose to use 2000 and above numbers for such custom error codes and error messages.

In the following code sample, the setting measurepoint and disabling device event are monitored.

```java
 client.setArrivedMsgHandler(MeasurepointSetCommand.class, (MeasurepointSetCommand command, List<String> argList)->{
    boolean success = true;
    if(success){
        return MeasurepointSetReply.builder().build();
    }
    else {
        return MeasurepointSetReply.builder()
                .setCode(2000)
                .setMessage("handle the measurepoint set command failed")
                .build();
    }
});

client.setArrivedMsgHandler(SubDeviceDisableCommand.class, (SubDeviceDisableCommand command, List<String> argList)->{
    //if you donnot want to reply the message ,  just return null
    System.out.println(command);
    return null;
});
```

.. note:: If the user responds a null reply, the device side does not respond after executing the callback method. If the user responds an effective reply, the SDK will serialize the reply and send it to the cloud automatically. If the callback method is executed successfully, the user can set a response code 200 or not. For failed execution, the user can set a customized error code 2000 or above to be sent to the cloud. 

<!--End-->