# Query Tags

Upstream
- Request TOPIC: `/sys/{productKey}/{deviceKey}/thing/tag/query`

- Reply TOPIC: `/sys/{productKey}/{deviceKey}/thing/tag/query_reply`

## Example Request Message

```
{
 "id": "123",
 "version": "1.0",
 "params": {
   "tags": ["tag1", "tag2"]
 },
 "method": "thing.tag.query"
}

```

## Example Response Message

```
{
 "id": "123",
 "code": 200,
 "data": {
   "tag1": "value1",
   "tag2": "value2"
 }
}

```

## Parameter Description

.. list-table::
   :widths: auto

   * - Parameter
     - Type
     - Description
   * - id
     - Long
     - Message ID. Reserved parameter for future use.
   * - version
     - String
     - Version of the protocol. Current version is 1.0.
   * - params
     - Object
     - Parameters used for querying tags
   * - tags
     - Object
     - The unique identifiers of the tags.
       When not specified, the request will query all tags.
   * - method
     - String
     - The method of the request.
   * - code
     - Integer
     - Response code. &ldquo;200&rdquo; indicates that the requested operation is executed successfully.

<!--end-->
