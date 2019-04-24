# Dynamic Number Insertion

:warning: **DRAFT** :warning:

## Create a Pool of Labeled Numbers

1. Create a pool of phone numbers for use in targeted ads. These should all be company numbers.
1. Use `phoneNumber.label` field to hold custom information. Update `phoneNumber.label` using the API below.

APIs:

```
PUT /restapi/v1.0/account/{accountId}/phone-number/{phoneNumberId}

{
    "label" : "Company`s secret number"
}
```

## Listening to Incoming Calls

### Setup

1. Create a subscription to listen to incoming calls for the account. Event filter: `/restapi/v1.0/account/{accountId}/telephony/sessions`
1. Build reverse look-up cache of phoneNumbers to campaignIds in the label property that is updated whenver campaign Ids are updated.

### Runtime

1. For each incoming call event, look up `body.parties[x].from.phoneNumber` and map to campaignId.
1. For each incoming call event, save `sessionId` and `recordingId` to retrieve additional info.

APIs:

* Account Telephony Sessions Event Reference:
  * https://developers.ringcentral.com/api-reference#Account-Telephony-Sessions-Event-Beta

## Retrieving an Associated Call Recording

Pull the recordings:

https://stackoverflow.com/questions/55071991/how-can-i-retrieve-a-ringcentral-call-recording-from-a-monitored-incoming-call