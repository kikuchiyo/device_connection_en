# Report Tags

Upstream
- Request TOPIC: `/sys/{productKey}/{deviceKey}/thing/tag/update`

- Reply TOPIC: `/sys/{productKey}/{deviceKey}/thing/tag/update_reply`

## Example Request Message

```
{
 "id": "123",
 "version": "1.0",
 "params": [
 {
 "tagKey": "Temperature",
 "tagValue": "36.8"
 }
 ],
 "method": "thing.tag.update"
}

```

## Example Response Message

```
{
 "id": "123",
 "code": 200,
 "data": {}
}

```

## Parameter description

.. list-table::
   :widths: 20 20 20 40

   * - Parameter
     - Type
     - Occurrence
     - Description
   * - id
     - Long
     - Optional
     - Message ID. Reserved parameter for future use.
   * - version
     - String
     - Mandatory
     - Version of the protocol. Current version is 1.0.
   * - params
     - Object
     - Mandatory
     - Parameters used for reporting tags. A request can carry a maximum of 200 parameters.
   * - method
     - String
     - Mandatory
     - The method of the request.
   * - tagKey
     - String
     - Mandatory
     - Tag name.
        + Maximum of 100 characters in length.
        + Support lowercase characters (a-z), uppercase characters (A–Z), numbers (0-9), and underline (_).
        + Start with an letter or underline (_).
   * - tagValue
     - String
     - Mandatory
     - The value of the tag.
   * - code
     - Integer
     - Mandatory
     - Response code. &ldquo;200&rdquo; indicates that the requested operation is executed successfully.
   * - data
     - JSON
     - Optional
     - Detailed returned information in JSON format.

<!--end-->
