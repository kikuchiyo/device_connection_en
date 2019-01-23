# Creating Data Parsing Script

When creating a product, if you select **Custom** for the **Data Type** field, the device can send data in any format (like binary data) to the EnOS Cloud. If this is the case, you will need to create data parsing script to encode and decode the upstream and downstream data. This topic describes how to edit and debug the script in the EnOS Cloud, and how to upload it to the EnOS runtime environment.

## Procedure

1. In the EnOS Console, select **Device Management** > **Product**.

2. In the table of created products, for the target product, click **View** to open the **Product Details** page.

3. Click the **Data Parsing** tab to open the data parsing page.

4. In **Edit Script**, enter the script code. JavaScript is currently supported.

5. Click **Save Draft** at the bottom of the page for the system to save the results of this edit. The next time you log in and enter this screen, you will be prompted with the last-saved draft, and you can choose to resume editing or delete the draft.

   - The draft will not enter the script parsing runtime environment, and saving the draft does not affect the formal scripts you have already submitted;
   - Each time you save a draft, it will overwrite the last saved one.

6. In **Analog input**, enter the mockup data, and select the simulation type as **Sent data** or **Receive data**.

   - **Sent data**: In the text box, enter the passthrough binary data to be sent and click **Run**. The data format will be converted from binary to JSON according to the script rules, and you can view the parsing result of the passthrough data.
   - **Receive data**: In the text box, enter data in JSON format and click **Run**. The data format will be converted from JSON to binary according to the script rules, and you can view the parsed result.

7. Click **Run** to test the script; you can view the results in the **Running Results** section. If there is any error in the script, you will be prompted that the run has failed.

8. After you have checked that the script is working as intended, click **Submit** to submit the script to the runtime environment.

## Results

When EnOS Cloud transmits data with devices, the script will be automatically invoked to parse and convert data format.
