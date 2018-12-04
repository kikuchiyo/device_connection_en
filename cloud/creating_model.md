# Creating Model

A model is an abstraction of the product's features, and defines what the product is, what it can do, and what services it can provide. This article describes how to create a model.

## Before You Start
The features required for the model have been designed. For information on how to design the features of the model, please refer to [Thing Model Overview](../model_overview)

## About This Task

Configure all the features in EnOS according to the defined thing model.
- Attributes
- Measure Points
- Service
- Event

## Step 1: Create a Model

1. In the EnOS Console, select **Access Management > Model Management**.
2. Click **New Model** at the top right of the page, and provide the following settings on the **Creating Model** page:
  - **Identifier**: A unique identifier of the model.
  - **Model Name**: The name of the model; duplicate name is not allowed under the same organization.
  - **Category**: Static extension info of the product, Such as manufacturer, and device model.
  - **Create From**:
    - None: Do not configure specific attributes for now. Manually define the elements after the template is created.
    - Copy: Copy all the information of the source model. There is no association between the source model and the model created by copying it.
    - Inherit: Copy all the information of the source model. The created model is associated with the source model.    
      - The child model will inherit all the elements of its parent model, and the child template cannot modify the elements in the parent template.
      - The child model can add new elements based on the parent model, but it needs to use a different name from the parent model.
      - The child model can be further inherited to support multi-level inheritance.
      - Changes to the elements in the parent model will affect the child template.
  - **Source Model**: The model selected for copying or the inherited parent model.
  - **Description**: A detailed description of the model.
3. Click **Confirm** to complete the operation.

## Step 2: Define Elements for the Model

1. Find the model that needs feature definition and click **View**.
2. Select the **Feature Definition** tag and click **Add** to set one or more elements according to the product attributes.

### Adding Attributes

1. On the **Add Feature** page, select the attribute in **Feature Type** section and provide the following settings:
   - **Name**: The name of the attribute; duplicate name is not allowed under the same module.
   - **Name (en)**: if the **Name** is in Chinese, an English name can be set here. You can ignore this setting if the **Name** is in English.
   - **Identifier**: A unique identification code for the feature; duplicate identifier is not allowed under the same organization. This identifier value in JSON format is used as a key by the device to send attribute data. The cloud will verify the identifier before deciding whether to receive the data.
   - **Data Type**: The data type of this attribute.

     + int, float, double: Information such as the default value and the data unit shall be defined.
     + enum: The parameter value of enum items and parameter description shall be defined.
     + bool: Boolean value shall be defined as 0 or 1.
     + string: A default value, the string type and string length shall be defined.
     + timestamp: The timestamp is in the form of a UTC timestamp string (in milliseconds).
     + date: The format of date is yyyy-MM-dd HH:mm:ss.
     + struct: A JSON structure defined by **Parameter Name**, **Identifier**, **Data Type** and **Unit**.
     + array: **Type** shall be defined. Make sure that the same type is used in the same array.

   - **Required**: If set to "Required", the parameter must be provided when creating a new device under this product.
   - **Description**: A description of the attribute.

2. Click **Confirm** to finish creating the attribute.

3. To create more attributes, repeat the above steps.

### Adding Measure Points

Below is the configuration information in the "Measure Points" page:
1. On the **Add Feature** page, select the measure point in the **Feature Type** section and provide the following settings:
   - **Name**: The name of the measure point; duplicate name is not allowed under the same module.
   - **Name (en)**: If the name is in Chinese, an English name can be set here. You can ignore this setting if the **Name** is in English.
   - **Identifier**: A unique identification code for the feature; duplicate identifier is not allowed under the same organization. This identifier value in JSON format is used as a key by the device to send attribute data. The cloud will verify the identifier before deciding whether to receive the data.
   - **Whether It Is a Quality Indicator**: Whether the measure point is an indicator of the data quality. If set to **Yes**, the configurations are as follows:

      + Quality Indicator: Data quality indicator in the form of array that is predefined by the system; cannot be changed. You can click **View** to see the predefined quality indicator parameters as well as their descriptions.
      + Value: Sets the data type of the measure point. Only three types are supported: int, float, and double.

   - **Data Type**: If the test is not about quality indicator, the data type of the measure point shall be configured.
   -
     + int, float, double: Information such as the default value and the data unit shall be defined.
     + enum: The parameter value of enum items and parameter description shall be defined.
     + bool: Boolean value shall be defined as 0 or 1.
     + string: A default value, the string type and string length shall be defined.
     + timestamp: The timestamp is in the form of a UTC timestamp string (in milliseconds).
     + date: The format of date is yyyy-MM-dd HH:mm:ss.
     + struct: A JSON structure defined by **Parameter Name**, **Identifier**, **Data Type** and **Unit**.

   - **Tags**: Tags can be used to describe a measure point; depending on the needs, you can flexibly identify a measure point, such as its type, group, and priority.
   - **Description**: A description of the measure point.

2. Click **Confirm** to create a measure point.

3. To create more measure points, repeat the above steps.

### Adding Service

1. On the **Add Feature** page, select a service in **Feature Type** section and provide the following settings:
   - **Name**: The name of the measure point; duplicate name is not allowed under the same module.
   - **Name (en)**: If the name is in Chinese, an English name can be set here.
   - **Identifier**: A unique identification code for the feature; duplicate identifier is not allowed under the same organization. This identifier value in JSON format is used as a key by the device to send attribute data. The cloud will verify the identifier before deciding whether to receive the data.
   - **Invoke Method**: The way to invoke the service.
     + Synchronous: The cloud invokes the service and waits for the device to reply. If no reply is received, the invocation times out.
     + Asynchronous: The cloud invokes the service and returns immediately; the reply message from the device is obtained asynchronously.
   - **Input Parameters**: Click **New Parameter** to configure the name, identifier, data type, and data unit of the input parameter of the service.
   - **Output Parameters**: Click **New Parameter** to configure the name, identifier, data type, and data unit of the output parameter of the service.
   - **Description**: A description of the service.

2. Click **Confirm** to create the service.

3. To create more services, repeat the above steps.

### Adding Event

1. On the **Add Feature** page, select an event in **Feature Type** section and provide the following settings:
   - **Name**: The name of the measure point; duplicate name is not allowed under the same module.
   - **Name (en)**: If the name is in Chinese, an English name can be set here.
   - **Identifier**: A unique identification code for the feature; duplicate identifier is not allowed under the same organization. This identifier value in JSON format is used as a key by the device to send attribute data. The cloud will verify the identifier before deciding whether to receive the data.
   - **Severity**:
     + Info: Refers to general notifications reported by devices, such as a notification on job completion.
     + Warning: Warning messages. Emergencies or exceptions reported voluntarily by a running device; these events have a high priority. You can perform service logic processing and statistical analysis depending on the severity of the events.
     + Error: Error messages. Emergencies or exceptions reported voluntarily by a running device; these events have a high priority. You can perform service logic processing and statistical analysis depending on the severity of the events.
   - **Output Parameters**: Click **New Parameter** to configure the name, identifier, data type, and data unit of the output parameter of the service.
   - **Description**: A description of the event.

2. Click **Confirm** to create the event.

## Step 3: (Optional) Add a Tag
A tag describes the common information shared by models of the same type. It can be used to distinguish model objects by describing their categories such as domain, type, and scope. For example, by adding a **domain:solar** tag to a model, you are specifying that the model falls in the solar field.

1. In the EnOS Console, select **Access Management > Model Management**.
2. Click **View** next to the model to be added, and click **Edit** in the Tags section to add a tag. A tag is made up of a key-value pair (key:value).

## Results

When feature definition is completed, the system will automatically generate a model for the product in JSON format.

## Related Information

- [Model Overview](../model_overview)
- [Creating Product](creating_product)
