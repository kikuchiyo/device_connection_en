# Creating Alert Types

This topic instructs how to create the alert types and subtypes for your assets via the **Asset Alert** page on EnOS Console.

Alert types are defined to distinguish status of assets and possible causes of alerts, so that you can better monitor the status of your assets. To define an alert type, you need to provide an ID, description, and tag for it.

## Before You Start

For a specific domain device, alert types are typically found in its instructions, but you can also customize the definitions according to your business needs or best practices in the domain.

For example, a padmount transformer, potential security risks exist when the temperature exceeds 85 degree Centigrade. Becasue the alert is defined based on the temperature threshold, you can define it as an "exceeding limit" alert.

## Configuring Alert Types

You can define types and subtypes to facilitate the alert management of your assets. An alert type can comprise several subtypes.

### Defining an Alert Type

1. Click **Asset Alert > Alert Type** from the left navigation panel of the EnoS Console.

2. Click **New Type** and provide an ID, description, and tag (optional) for the alert type.

   .. image:: media/create_alert_type.png
      

### Defining a Subtype

After an alert type is created, you can create a subtype for it to subdivide the definition of alert types.

1. In the table of alert types, click the **Create Subtype** icon from the **Operations** column.

2. Provide an ID, description, and tag (optional) for the subtype.

.. image:: media/create_alert_subtype.png
   

<!--end-->
