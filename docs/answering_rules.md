# Answering Rules

Each RingCentral extension has two answering rule resources, one for business hours and another for after hours. These can be configured by end-users using the RingCentral Online Account Portal under extension Call Handling & Forwarding.

The answering rule API endpoint is:

* `v1.0/account/~/extension/~/answering-rule/`

There are standard rules for `business-hours-rule` and `after-hours-rule` as well as support for custom rules. Standard rule endpoints are shown below:

* `v1.0/account/~/extension/~/answering-rule/business-hours-rule`
* `v1.0/account/~/extension/~/answering-rule/after-hours-rule`

## Read Answering Rule List

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `v1.0/account/{accountId}/extension/{extensionId}/answering-rule/` | Get extension rule list |

```bash
GET /restapi/v1.0/account/11111111/extension/22222222/answering-rule HTTP/1.1
Accept: application/json
Authorization: Bearer MyAccessToken

{
  "uri": "https://platform.devtest.ringcentral.com/restapi/v1.0/account/11111111/extension/22222222/answering-rule?page=1&perPage=100",
  "records": [
    {
      "uri": "https://platform.devtest.ringcentral.com/restapi/v1.0/account/11111111/extension/22222222/answering-rule/33333333",
      "id": "33333333",
      "type": "Custom",
      "name": "My Custom Rule 1",
      "enabled": true,
      "callers": [
        {
          "callerId": "16505551212"
        }
      ],
      "callHandlingAction": "ForwardCalls"
    },
    {
      "uri": "https://platform.devtest.ringcentral.com/restapi/v1.0/account/11111111/extension/22222222/answering-rule/business-hours-rule",
      "id": "business-hours-rule",
      "type": "BusinessHours",
      "enabled": true,
      "callHandlingAction": "ForwardCalls"
    }
  ],
  "paging": {...},
  "navigation": {...}
}
```

## Read an Answering Rule

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `v1.0/account/{accountId}/extension/{extensionId}/answering-rule/{ruleId}` | Get a rule |

### Example Request

```bash
GET /restapi/v1.0/account/11111111/extension/22222222/answering-rule/business-hours-rule HTTP/1.1
Accept: application/json
Authorization: Bearer MyAccessToken
```

### Example Response

```bash
HTTP/1.1 200 OK
Content-Type: application/json

{
    "uri": "http://platform.ringcentral.com/restapi/v1.0/account/11111111/extension/22222222/answering-rule/business-hours-rule",
    "id": "business-hours-rule",
    "type": "BusinessHours",
    "enabled": true,
    "schedule": {
        "ref": "BusinessHours"
    },
    "callHandlingAction": "ForwardCalls",
    "forwarding": {
        "notifyMySoftPhones": true,
        "notifyAdminSoftPhones": false,
        "softPhonesRingCount": 1,
        "ringingMode": "Sequentially",
        "rules": [
            {
                "index": 1,
                "ringCount": 4,
                "forwardingNumbers": [
                    {
                        "uri": "http://platform.ringcentral.com/restapi/v1.0/account/11111111/extension/22222222/forwarding-number/33333333",
                        "id": "33333333",
                        "phoneNumber": "+16505551212",
                        "label": "My Cisco SPA-303 Desk Phone"
                    }
                ]
            },
            {
                "index": 2,
                "ringCount": 8,
                "forwardingNumbers": [
                    {
                        "uri": "http://platform.ringcentral.com/restapi/v1.0/account/11111111/extension/22222222/forwarding-number/44444444",
                        "id": "44444444",
                        "phoneNumber": "+4155551212",
                        "label": "Home"
                    }
                ]
            },
            {
                "index": 3,
                "ringCount": 12,
                "forwardingNumbers": [
                    {
                        "uri": "http://platform.ringcentral.com/restapi/v1.0/account/11111111/extension/22222222/forwarding-number/55555555",
                        "id": "55555555",
                        "phoneNumber": "+12125551212",
                        "label": "Mobile"
                    }
                ]
            }
        ]
    },
    "greetings": [
        {
            "type": "Voicemail",
            "prompt": {
                "id": "0",
                "type": "message",
                "name": "No One Available"
            }
        },
        {
            "type": "Introductory"
        },
        {
            "type": "AudioWhileConnecting",
            "prompt": {
                "id": "6",
                "type": "music",
                "name": "Acoustic"
            }
        },
        {
            "type": "ConnectingMessage",
            "prompt": {
                "id": "3",
                "type": "message",
                "name": "Forward hold 1"
            }
        }
    ],
    "screening": "Never",
    "voicemail": {
        "enabled": true,
        "recipient": {
            "uri": "http://platform.ringcentral.com/restapi/v1.0/account/11111111/extension/22222222",
            "id": 22222222
        }
    }
}
```

## Update an Answering Rule


## Delete an Answering Rule

| Method | Endpoint | Description |
|--------|----------|-------------|
| `DELETE` | `v1.0/account/{accountId}/extension/{extensionId}/answering-rule/{ruleId}` | Delete a rule |

## Update a Forwarding Number

Permissions needed: EditExtensions
The business and after hours rules can forward calls to a set of forwarding numbers. To update the phone number used, identify the forwarding number in the list of rules and then update the phone number of that resource using a HTTP PUT request to the endpoint updating the phoneNumber property.

An update can be written as follows:

| Method | Endpoint | Description |
|--------|----------|-------------|
| `PUT` | `v1.0/account/{accountId}/extension/{extensionId}/forwarding-number/{forwardingNumberId}` | Update a forwarding number |

### Example Request

```bash
PUT /restapi/v1.0/account/11111111/extension/22222222/forwarding-number/33333333 HTTP/1.1
Accept: application/json
Authorization: Bearer MyAccessToken
Content-Type: application/json

{
  "phoneNumber": "+16505551212"
}
```
