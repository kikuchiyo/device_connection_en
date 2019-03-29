# NTP Service

You can use the following sample code to apply the NTP service:

```java
    public static void main(String[] args) {
        MqttClient client = new MqttClient(new FileProfile());
        System.out.println("local :" + System.currentTimeMillis());
        System.out.println("fix : " + (client.getExtServiceFactory().getNtpService().getFixedTimestamp()));
        System.out.println("fix : " + (client.getExtServiceFactory().getNtpService().getFixedTimestamp(System.currentTimeMillis())));
        //Use the NTP service event to post measure point data
        MeasurepointPostRequest request = MeasurepointPostRequest.builder()
                        .addMeasurePoint("point1", random.nextInt(100))
                        .setTimestamp(client.getExtServiceFactory().getNtpService().getFixedTimestamp())
                        .build();
        try {
            MeasurepointPostResponse rsp = client.publish(request);
            System.out.println("-->" + rsp);

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
```