# Creating a Data Parsing Script

When the **Data Format** of the product is defined as transparent, the device can send data in any format (e.g., binary data) to the EnOS Cloud. If this is the case, you will need to create a data parsing script to encode and decode the uplink and downlink data.  This article describes how to edit and debug the script in the EnOS Cloud, as well as how to upload it to the EnOS runtime environment.

## Procedure

1. In the EnOS Console, select **Access Management > Product Management**.

2. Find the product to which you need to link the data parsing script, and then click the **View** next to it and select the **Script Parsing** tag.

3. In **Edit Script**, enter the script code. JavaScript is currently supported.

4. Click **Save Draft** at the bottom of the page for the system to save the results of this edit. The next time you log in and enter this screen, you will be prompted with the last-saved draft, and you can choose to resume editing or delete the draft.
  - The draft will not enter the script parsing runtime environment, and saving the draft does not affect the formal scripts you have already submitted;
  - Each time you save a draft, it will overwrite the last saved one.

5. In **Simulation Input**, enter the simulation data. You can also select the simulation type as **Report Data on Device Send** or **Accept Data on Device**.
   - **Report Data on Device**: In the dialog box, enter the binary data to be sent transparently and click **Run**. The data format will be converted from binary to JSON according to the script rules, and you can view the parsing result of the transparently transmitted data in the running results area.
   - **Accept Data on Device**: In the dialog box, enter data in JSON format and click "Run". The data format will be converted from JSON to binary according to the script rules, and you can view the parsed data in the running results section.

5. Click **Run** to test the script; you can view the results in the **Running Results** section. If there is any error in the script, you will be prompted that the run has failed.
   - **Report Data on Device**: Binary data that need to be transmitted transparently will be converted to JSON format according to the script rules and displayed in the **Running Results** section.
   - **Accept Data on Device**: Data in JSON format will be converted to binary data according to the script rules and displayed in the **Running Results** section.

6. After you have checked that the script is working as intended, click **Submit** to submit the script to the runtime environment.

## Results

The script will be automatically invoked to parse and convert data when EnOS and the device are transmitting data on the uplink or downlink.
