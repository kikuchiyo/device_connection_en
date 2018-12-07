# Thing Model Overview

The thing model is the abstraction and digitization of the physical objects in the physical world. A thing model is the summary of the features of the objects that are connected to the EnOS Cloud, including attributes, measure points, services and events of the device.

In EnOS, defining thing model means defining the features of the product. The thing model describes what the product is, what it can do, and what services it can provide. On the EnOS platform, the description language of the thing model is in JSON format, and you can assemble and report the device data according to the syntax of the thing model.


## Thing Model Elements
You can define the following elements to define a thing model according to the actual needs of the product.

<table>
   <tr>
      <th>Model elements</th>
      <th>Description</th>
      <th>Instance</th>
    </tr>
    <tr>
      <td>Attribute</td>
      <td>Describes the static attribute of the device. You can define the name and identifier of the static attribute. The attribute name is a descriptive string that allows Chinese input.</td>
      <td>Name, model, location, design parameters, longitude, etc.</td>
    </tr>
    <tr>
      <td>Measure point</td>
      <td>Describes the runtime state of the device. You can define the name of the measure points as well as its identifier. The measure point name is a descriptive string that allows Chinese input.</td>
      <td>Temperature, pressure, current, voltage, various states, etc.</td>
    </tr>
        <tr>
      <td>Service</td>
      <td>A capability or method that can be called externally. You can define its input and output parameters. Compared with an attribute, you can achieve more complex business logic through a command.</td>
      <td>Command to issue, job to perform, etc.</td>
    </tr>
        <tr>
      <td>event</td>
      <td>The event that can occur when the device is running. An event generally contains notification information that needs to be externally perceived and processed, and may include multiple output parameters.</td>
      <td>Alerts, state changes, information about the completion of a job, or the temperature of a device when a failure or alert occurs, etc. An event can be subscribed and pushed.</td>
    </tr>
</table>

## Model Relationship

A model can be created from a source model through: **Clone** and **Inherit**. The difference of the two creating modes are mainly reflected in the model relationship.

**Clone**

For models created from the **Clone** mode, the new model has exactly the same four elements as the source model. The two models are independent from each other, and changes to one model will not affect the other.

**Inherit**

For models created from the **Inherit** mode, we define the newly created models as the **Sub Model** and the source model is the **Parent Model**. The sub model has the following main characteristics:
- The sub model inherits all the features of the parent model, and the inherited elements cannot be modified.
- The sub model can be inherited again, and supports multi-level inheritance relationships.
- The sub model can have independent elements, but the newly added elements in the sub model shall not have the same name as the elements of all parent models.
- When the four elements of the parent model are changed, the sub model's four elements inherited from the parent model are changed synchronously to remain consistent with the parent model.

## Model Permission
The read and write permissions for the model can be divided into two categories: **Public Model** and **Private Model**.

**Public Model**

The public models are the domain standard models that are accumulated on EnOS and are made public to all organization units by EnOS. All OUs have read permission but no write permission to the public models.

**Private Model**

The private models are created by the developers in their own OU. Private models are not open to the public and are visible only within the organization. The developers in the organization have read and write permissions to the private models.
