# Thing Model Overview

The thing model is the abstraction and digitization of the physical objects in the physical world. The thing model is a summary of the cloud-side functions of the objects connected to the EnOS Cloud, including attributes, measure points, services and events of the device.

In EnOS, defining thing model means defining the functions of the product. The thing model describes what the product is, what it can do, and what services it can provide. On the EnOS platform, the description language of the thing model is in JSON format, and you can assemble and report the device data according to the syntax of the thing model.


## Thing Model Elements
The user can define the following elements to define an thing model according to the actual needs of the product.

<table>
   <tr>
      <th>Model elements</th>
      <th>Description</th>
      <th>Instance</th>
    </tr>
    <tr>
      <td>Attribute</td>
      <td>Describes the static attribute of the device. The static attribute allows the user to customize the name of the attribute as well as the corresponding identifier. The name is equivalent to a description that allows Chinese input.</td>
      <td>Name, model, location, design parameters, longitude, etc.</td>
    </tr>
    <tr>
      <td>Measure point</td>
      <td>Describes the operating state of the device. The measure point allows the user to customize the name of the measuring point as well as its identifier. The name is equivalent to a description that allows Chinese input.</td>
      <td>Temperature, pressure, current, voltage, various states, etc.</td>
    </tr>
        <tr>
      <td>Service</td>
      <td>A capability or method that can be called externally. Both its input and output parameters can be configured. Compared with an attribute, a service can perform more complex business logic with one instruction.</td>
      <td>Issued instructions, performed jobs, etc.</td>
    </tr>
        <tr>
      <td>event</td>
      <td>An event is one occurring when the device is running. An event generally contains notification information that needs to be externally perceived and processed, and may include multiple output parameters.</td>
      <td>Alarms, status changes, information about the completion of a job, or the temperature of a device when a failure or alarm occurs, etc. An event can be subscribed and pushed.</td>
    </tr>
</table>

## Model Relationship

There are two modes for creating a model: **Clone** and **Inherit**. The difference of the two creating modes are mainly reflected in the model relationship.



**Clone**

For the model created by the **Clone** mode, the new model has exactly the same four elements as the copied model. The two models are independent of each other, and the any change to one model will not affect the other one.


**Inherit**

For model created by the **Inherit** mode, we define the newly created models as **Sub Model** and the inherited model as **Parent Model**. The sub model has the following main features:
- The sub model inherits all the features of the parent model, and the inherited elements cannot be modified.
- The sub model can be inherited again, and supports multi-level inheritance relationships.
- The sub model can create independent elements, but the newly added elements in the sub model shall not have the same name as the elements of all parent models.
- When the four elements of the parent model are changed, the sub model's four elements inherited from the parent model are changed synchronously to remain consistent with the parent model.



## Model Permission
The read and write permissions for the model can be divided into two categories: **Public Model** and **Private Model**.

**Public Model**

Open to all organizations, with read access and without write access. The public models are some of the domain standard models that are deposited on the EnOS platform and are made public to all organizations by EnOS.


**Private Model**

The models created by the developers in their own organization are all private models. They are not open to the outside and are only visible within the organization. The developers in the organization have the model read and write permissions.
