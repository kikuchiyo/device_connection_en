# Creating Alert Rules

This topic instructs how to create the triggering rules of an alert.

You can define alert triggering rules for a data measuring point of a domain or the communication model of a device point.

In wind turbine example, you can define an alert triggering rule when the wind speed is over 30m/s, the severity level, and the content to report when the alert occurs.

## Before You Start

Ensure that the alert content to be used by the triggering rule is created. For more information, see [Creating Alert Content](create_alert_content).

## Procedure

1. Click **Asset Alert > Alert Rule** from the left navigation panel of the EnoS Console.

2. Click the **New Rule** button to define a new alert triggering rule.

   .. image:: media/create_alert_rule.png


   - **Select model**

     Select the asset model that is defined in the **Model** section. For more information, see [Model Management](../model/model_overview).

   - **Condition**

     Select a triggering condition for the alert rule and enter the corresponding value or value scope for the condition.

   - **Scope**

     Select the scope of the asset to which the alert applies to according to the selected asset model. The triggering rule can apply to a whole station or specific device of the station.

   - **Alert Content**

     Select alert content for the rule from the list of defined alert content. An alert content can be assigned to multiple triggering rules.

   - **Alert Severity**

      Select an alert severity level from the list of defined severity levels according to your business needs.

   - **Alert Rule for Recovery Only**

     Specify if the triggering rule is used for a recovery event only. A recovery alert represents a normal condition, which can be used to end the raised alerts.
