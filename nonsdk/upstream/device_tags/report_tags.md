# Report Tags

Upstream
- Request TOPIC: /sys/{productKey}/{deviceKey}/thing/tag/update

- Reply TOPIC: /sys/{productKey}/{deviceKey}/thing/tag/update_reply

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

<table>
  <tr>
    <td>Parameter</td>
    <td>Type</td>
    <td>Occurrence</td>
    <td>Description</td>
  </tr>
  <tr>
    <td>id</td>
    <td>Long</td>
    <td>Optional</td>
    <td>Message ID. Reserved parameter for future use.</td>
  </tr>
  <tr>
    <td>version</td>
    <td>String</td>
    <td>Mandatory</td>
    <td>Version of the protocol.  Current version is 1.0.</td>
  </tr>
  <tr>
    <td>params</td>
    <td>Object</td>
    <td>Mandatory</td>
    <td>Parameters used for reporting tags. The maximum items are 200.</td>
  </tr>
  <tr>
    <td>method</td>
    <td>String</td>
    <td>Mandatory</td>
    <td>The method of the request.</td>
  </tr>
  <tr>
    <td>tagKey</td>
    <td>String</td>
    <td>Mandatory</td>
    <td>Tag name.
      <ul>
        <li>Maximum 100 characters in   length</li>
        <li>Support lowercase characters ( a- z), uppercase characters( A – Z), numbers (0- 9), and underline (_). </li>
        <li>The tag name must start with  an letter or underline (_).</li>
      </ul></td>
  </tr>
  <tr>
    <td>tagValue</td>
    <td>String</td>
    <td>Mandatory</td>
    <td>The value of the tag.</td>
  </tr>
  <tr>
    <td>code</td>
    <td>Integer</td>
    <td>Mandatory</td>
    <td>Response code. &ldquo;200&rdquo; indicates the request is   executed successfully.</td>
  </tr>
  <tr>
    <td>data</td>
    <td>String</td>
    <td>Optional</td>
    <td>Detailed information of the sub-device, in JSON format.</td>
  </tr>
</table>
