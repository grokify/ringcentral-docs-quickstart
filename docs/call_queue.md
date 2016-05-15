# Call Queue

Call queues are ways to have multiple people response to incoming calls. Some characteristics of call queues include:

## Creating a Call Queue

Creating a call queue is performed in the Online Account Portal under groups.

## Get Call Queue List

The List Extensions endpoint can be used to retrieve a list of call queues, known as departments via the API.

| Endpoint | Description |
|----------|-------------|
| `account/{accountId}/extension?type=Department` | Get a list of call queues, aka departments |

### Example Request

```bash
GET /restapi/v1.0/account/~/extension?type=Department
Accept: application/json
Content-Type: application/json
Accept-Language: en-US
Authorization: Bearer MyToken
```

### Example Response

```bash
HTTP/1.1 200 OK
Content-Type: application/json

{"uri"=>
  "https://platform.devtest.ringcentral.com/restapi/v1.0/account/11111111/extension?type=Department&page=1&perPage=100",
 "records"=>
  [{"uri"=>
     "https://platform.devtest.ringcentral.com/restapi/v1.0/account/11111111/extension/22223333",
    "id"=>22223333,
    "extensionNumber"=>"201",
    "contact"=>
     {"firstName"=>"Sales Queue", "email"=>"john.ringforce@gmail.com"},
    "name"=>"Sales Queue",
    "type"=>"Department",
    "status"=>"Enabled",
    "permissions"=>
     {"admin"=>{"enabled"=>false}, "internationalCalling"=>{"enabled"=>false}},
    "profileImage"=>
     {"uri"=>
       "https://platform.devtest.ringcentral.com/restapi/v1.0/account/130709004/extension/131085004/profile-image"}}],
 "paging"=>{...}
}
```

## Adding and Removing Queue Members

Users can be added and removed using the `account/~/department/bulk-assign` endpoint and the extension ids of interest.

| Endpoint | Description |
|----------|-------------|
| `account/{accountId}/department/bulk-assign` | Add and remove multiple users from one or more departments |

### Example Request

```bash
POST /restapi/v1.0/account/~/department/bulk-assign
Accept: application/json
Content-Type: application/json
Authorization: Bearer MyToken

{
  "items": [
    {
      "departmentId": "22223333",   
      "addedExtensionIds": [
        "11112222", "11113333"
      ],
      "removedExtensionIds": [
        "11114444", "11115555"
      ]
    }, 
    {
      "departmentId": "22224444",   
      "addedExtensionIds": [
        "11112222", "11113333"
      ]
    }
  ] 
}
```

### Example Response

```bash
HTTP/1.1 204 No Content
Content-Type: application/json
Content-Language: en-US
```

## List Queue Members

To get the members of a queue, call the department members endpoint.

| Endpoint | Description |
|----------|-------------|
| `v1.0/account/{accountId}/department/{departmentId}/members` | Get department members |

### Example Request

```bash
POST /restapi/v1.0/account/11112222/department/22223333/members
Accept: application/json
Authorization: Bearer MyToken
```

### Example Response

```bash```bash
HTTP/1.1 200 OK
Content-Type: application/json

{
  "uri": "https://platform.devtest.ringcentral.com/restapi/v1.0/account/11111111/department/22223333/members?page=1&perPage=100",
  "records": [
    {
      "uri": "https://platform.devtest.ringcentral.com/restapi/v1.0/account/11111111/extension/11112222",
      "id": 11112222,
      "extensionNumber": "101"
    },
    {
      "uri": "https://platform.devtest.ringcentral.com/restapi/v1.0/account/11111111/extension/11113333",
      "id": 11113333,
      "extensionNumber": "102"
    }
  ],
  "paging": {...}
  "navigatin": {...}
}
```

## Get Extension Queue Presence

Queue presence is set by the extension's presence `dndStatus` property which can be set to one of four values:

1. `TakeAllCalls`
1. `DoNotAcceptAnyCalls`
1. `DoNotAcceptDepartmentCalls`
1. `TakeDepartmentCallsOnly`

| Endpoint | Description |
|----------|-------------|
| `v1.0/account/{accountId}/extension/{extensionId}/presence` | Get extension presence |

### Example Request

```bash
GET /restapi/v1.0/account/11112222/department/11112222/members
Accept: application/json
Authorization: Bearer MyToken
```

### Enabling and Disabling Queue Membership Presence

To enable or disable an extensions membership presence, update the extensions

| Endpoint | Description |
|----------|-------------|
| `v1.0/account/{accountId}/extension/{extensionId}/presence` | Get extension presence |

### Example Request

```bash
PUT /restapi/v1.0/account/11112222/department/11112222/members
Accept: application/json
Authorization: Bearer MyToken

{
  "dndStatus": "DoNotAcceptDepartmentCalls"
}
```
