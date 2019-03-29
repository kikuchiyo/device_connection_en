# Delete Tags

Upstream

- Request TOPIC `/sys/{productKey}/{deviceName}/thing/tag/delete`

- Reply TOPIC `/sys/{productKey}/{deviceName}/thing/tag/delete_reply`

## Example Request Message

```
{
 "id": "123",
 "version": "1.0",
 "params": {
    "tags": ["tag1", "tag2"]
 },
 "method": "thing.tag.delete"
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

## Parameter Description

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
     - Version of the protocol. Current version is 1.0.
   * - params
     - List
     - Mandatory
     - Parameters used for deleting tags.
   * - tags
     - List
     - Mandatory
     - The unique identifier of the tags.<br>
       When not specified, no tag is deleted.
   * - method
     - String
     - Mandatory
     - The method of the request.
   * - code
     - Integer
     - Mandatory
     - Response code. &ldquo;200&rdquo; indicates that the requested operation is executed successfully.
   * - data
     - JSON
     - Optional
     - Detailed returned information in JSON format.


<!--end-->
