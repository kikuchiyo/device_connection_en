# Creating Alert Severity Levels

This topic instructs how to create alert severity levels for your assets via the **Asset Alert** page on EnOS Console.

To define an alert severity level, you need to provide an ID, description, and tag for it. The description of the alert severity supports globalization, so that you can define different languages of alert content.

## Before You Start

For a specific domain asset, the alert severity level definitions are typically found in its instructions; although you can customize the definitions according to your business needs or best practices in the domain.

For example, a padmount transformer, potential security risks exist when the temperature exceeds 85 degrees centigrade. Therefore, the severity level is *Warning* according to the device instructions. However, if the temperature exceeds 100 degrees centigrade, you can define the severity level as *Fault* because the device might stop working.

## Configuring Alert Severity

1. Click **Asset Alert > Alert Severity** from the left navigation panel of the EnoS Console.

2. Click **New Severity Level** and provide an ID, description, and tag (optional) for the corresponding severity level.

   .. image:: media/create_severity_level.png

The severity levels are mainly used for filtering the alert messages on GUI and analyzing the historical alerts. The domain application identifies the severity of the alert by the ID of the severity level.

### Example of Severity Levels

The following table shows a typical list of severity levels:

.. list-table::
   :widths: 50 50

   * - Severity Level ID
     - Description
   * - 398000001
     - Info
   * - 398000002
     - Warning
   * - 398000003
     - Fault

The severity level can be used as a key value in the application for a domain. The application needs to know the corresponding meaning of each severity level. For example, in your alert application for a domain, you can set to display only the alerts with severity _Warning_ and _Fault_ in the GUI. This feature is achieved by setting to show alerts with severity level ID _398000002_ or _398000003_.
