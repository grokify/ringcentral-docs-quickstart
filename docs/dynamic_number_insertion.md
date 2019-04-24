# Dynamic Number Insertion

:warning: **DRAFT** :warning:

## Create a Pool of Labeled Numbers

For this we will use one level of indirection and add the labels to the associated Extension to enable API-based updating of campaignIds. The phone numbers and associated extensions will be static. The campaignIds will be updatable by API.

1. Create a pool of phone numbers for use in targeted ads
1. Add phone numbers to a pool of extensions
1. Use Update Extension API to add campaignIds to each extension fields, e.g. `contact.department`, `contact.company`, `contact.jobTitle`, `contact.firstName`, `contact.lastName`

APIs:

* Update Extension API Reference:
  * https://developers.ringcentral.com/api-reference#User-Settings-updateExtension

## Listening to Incoming Calls

1. Create a subscription to listen to incoming calls for the account. Event filter: `/restapi/v1.0/account/{accountId}/telephony/sessions`
1. For each incoming call, look up `extensionId` in the Extension Info API in event to see if it is associated with campaign. If the call is of interest, save the event info including recordingId when present.

APIs:

* Account Telephony Sessions Event Reference:
  * https://developers.ringcentral.com/api-reference#Account-Telephony-Sessions-Event-Beta
* Get Extension Info API:
  * https://developers.ringcentral.com/api-reference#User-Settings-loadExtensionInfo

## Retrieving an Associated Call Recording

Pull the recordings:

https://stackoverflow.com/questions/55071991/how-can-i-retrieve-a-ringcentral-call-recording-from-a-monitored-incoming-call