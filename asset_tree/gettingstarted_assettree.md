# Getting Started with Asset Tree

This article describes how to create an asset tree and attach assets (such as devices) to the node of the asset tree through a sample scenario.

## Sample Scenario

A smart building project needs to collect `PM2.5`, `temperature`, `humidity` and `noise` data of the building. Each data has a corresponding sensor and these sensors are connected to a gateway. The gateway is responsible for collecting and forwarding data to EnOS Cloud.

Each building has different types of sensors. Some buildings have all of the four types of sensors, and some buildings might have only some of them.

In this scenario, we have two buildings, each building has the following sensors:

- **1#Building**
  - PM2.5
  - Temperature
  - Humidity
  - Noise

- **2#Building**
  - PM2.5
  - Temperature
  - Noise


## About the Task

According to the above scenarios, you need to create models for the types of assets listed in the sample and build an asset tree based on the asset hierarchy.

1. Create a model for each type of asset, you need to create the following six models:

    + The model that describes features of the devices:

      a. Model for PM2.5 sensor
         - Measuring point: PM2.5

      b. Model for temperature sensor
         - Measuring point: temperature

      c. Model for humidity sensor
         - Measuring point: humidity

      d. Model for noise sensor
         - Measuring point: noise

      e. Model for gateway device
         - Attribute: version
         - Measuring point: cpuRates

    + The model that describes the device group:

       f. Building model

       After creating the models, you can create the products based on the models.

2. Create the asset tree based on the asset hierarchy of this scenario.

    a. Create the root node of the asset tree for the organization.

    b. Create a child node **1#Building** under the root node.

    c. Create a child node for each sensor under the node **1#Building**.

    d. Repeat b and c for **2#Building**.

    If the gateway is treated as a device, you can attached the gateway device under the node **1#Building** and **2#Building** as shown in the following figure.

    The asset tree for this scenario is as follows:

    .. image:: ../media/building_tree.png   
       :width: 800px


## Procedure

### Step 1: Creating a Model

See [Creating a Model](../model/creating_model) to create models for each type of asset involved in the scenario.

### Step 2: Creating an Asset Tree

1. Create the root node of the asset tree.

   - In the EnOS Console, click **Asset Management** from the left navigation panel.
   - In the **Asset tree** page, click **+** in the upper left corner to create the root node of the asset tree.
      - The name of the root node is used as the name of this asset tree.
      - Generally, the root node of the asset tree is generally not a connected device.
      - If the node does not need a model, you can use the built-in model `<None>`, which has four empty elements, for root node.

2. After creating the root node, you can add a leaf node under the root node by the following approaches:
    - Create an asset based on the model
    - Add an existing asset to the asset tree

For information about the detailed settings, see [Creating an Asset Tree](creating_assettree).

## Related Information

- [Asset Tree Overview](assettree_overview)
- [Creating an Asset Tree](creating_assettree)
- [Managing an Asset Tree](managing_assettree)
