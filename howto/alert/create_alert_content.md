# Creating Alert Content

This topic instructs how to create an alert content record. To define content for an alert, you will provide the alert content ID, description, device model, alert type and subtype.

## Before You Start

Ensure the alert type that the alert content record belongs to is created. For more information, see [Creating Alert Types](create_alert_type).

## Procedure

1. Click **Asset Alert > Alert Content** from the left navigation panel of the EnoS Console.

2. Click **Add Content**, and provide the needed information for the alert content.

   .. image:: media/create_alert_content.png

   - **Content ID**: It is recommended to define a meaningful content ID to distinguish different types of the device. In the wind turbine example, you should create separate alerts for each DI value because the same DI value for different types of wind turbines can represent different state. Therefore, each DI value requires an event content record. You can name the event ID such as `GS_ST_001`, where:

     + `GS` represents the code of the device type or the branch.
     + `ST` represents the state of the device.
     + `001` represents the DI value of the device.

   - **Content Description**: Enter description of the alert content. In the wind turbine example, the description of the alert can be the description of the DI value.

   - **Model**: Select a device type from the list. In the wind turbines example, the device type is _turbines_.   

   - **Type / Subtype**: Select an alert type and subtype from the list of defined alert types.
