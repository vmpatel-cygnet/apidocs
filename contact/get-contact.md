# Get Contact

{% api-method method="post" host="\[PlatformAddress\]/api/1.0/contact?action=getContact" path="" %}
{% api-method-summary %}
Get Contact
{% endapi-method-summary %}

{% api-method-description %}
Get the contact details
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="integer" required=true %}
The contact's identifier
{% endapi-method-parameter %}

{% api-method-parameter name="useEventSortOrder" type="boolean" required=true %}
If true, the eventInvitations and eventRegistrations will be returned ordered by Event Start Date
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
This is an example response for getContact
{% endapi-method-response-example-description %}

```javascript
{
    "id":"25146",
    "firstName":"Test",
    "lastName":"User",
    "email":"user@test.com",
    "phone":"0455550000",
    "customFields":[
        {"fieldId":"102","displayName":"Dietary Requirements","value":[""]},
        {"fieldId":"103","displayName":"Shirt Size","value":["Medium"]}
    ],
    "groups":[
        {"contactId":"25146","groupId":"2481","joinDate":"2012-04-16 21:07:04"},
        {"contactId":"25146","groupId":"2485","joinDate":"2014-05-6 12:32:12"}
    ],
    "companies":[
        4,5,6
    ],
    "externalId":"59fc43b6726be"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

### Example Request

This example request will obtain the details of the contact with the id "6"

```javascript
{ 
  "id":6
}
```

## Returns

| **Property** | **Description** | **Type** |
| --- | --- |
| id | The unique identifier for the contact | integer |
| firstName | The contact’s first name | string |
| lastName | The contact’s last name | string |
| email | The contact’s email address | string |
| phone | The contact’s phone number | integer |
| status | The contact's [email status](get-contact.md#email-status) | enum |
| smsStatus | The contact’s [sms status](get-contact.md#sms-status) | enum |
| customFields | The custom field information for the contact. This is an array of fields, each an object with the [keys](get-contact.md#keys). | array |
| groups | The subscription group information for the contact. | array |
| companies | This will an array company ids to which the contact belongs. | array |
| externalId | This will be an external id of the contact | integer |
| modifiedDate | The modified date of the contact | date |
| eventInvitations | An array of events the contact has been invited to. Each element of the array is an object with [the event invitations fields](get-contact.md#event-invitations) | array |
| eventRegistrations | An array of events the contact has registered for. Each element of the array is an object with [the event registration fields](get-contact.md#event-registrations-details). | array |

### Status Options - Email Registration Status 

The status is the record of whether the contact has opted in to email communication.

| **\#** | **Description** |
| --- | --- |
| 1 | Subscribed |
| 2 | Unsubscribed |
| 3 | Bounced |
| 4 | Registering |
| 5 | No Marketing |

### Sms status

The sms status is the record of whether the contact has opted in to sms communication.

| **\#** | **Description** |
| --- | --- |
| 1 | Subscribed |
| 2 | Unsubscribed |
| 3 | Failed |
| 4 | No Marketing |

### Custom Fields Keys

| **Keys** |
| --- |
| fieldId |
| displayName |
| value |

### Event Invitations

| **Property** | **Description** |
| --- | --- |
| eventId | The event identifier of the invitation |
| eventCode | The code of the event of the invitation |
| eventStartDateTime | The timestamp the event is starting |
| inviteLinkYes | Invitation link for the Yes response for this contact to the event |
| inviteLinkNo | Invitation link for No response for this contact to the event |
| response | The contacts response to the invitation. [List of response values](get-contact.md#response-values). |

#### Event Invitations Response values

| **\#** | **Description** |
| --- | --- |
| U | Undecided |
| Y | Yes |
| N | No |

### Event Registrations Details

| **Property** | **Description** |
| --- | --- |
| eventId | The event identifier of the registration |
| eventCode | The code of the event of the registration |
| eventStartDateTime | The timestamp the event is starting |
| registrationId | The unique identifier of the registration |
| currentStatus | [The status of the registration](get-contact.md#registration-status) |
| confirmedDate | Timestamp of the date the registration was confirmed |
| isPaymentWaiting | If the registration is payment waiting or not |
| printTicketUrl | The URL the registrations tickets |
| printTicketUrlPdf | Link to the PDF for the registrations tickets |
| attendeeCount | Total number of attendees for this registration |
| invoiceUrl | The URL for the registration primary invoice |
| invoiceUrlPdf | Link to the PDF for the registration primary invoice |
| guestDetails | An array of objects with [the guest details.](get-contact.md#guest-details) |
| invoices | The list of invoices associated with the registration. Each element of the array is an object with [the invoice fields.](get-contact.md#invoice-details) |

#### Event Registration Status \(currentStatus\)

| **\#** | **Description** |
| --- | --- |
| 2 | Completed |
| 3 | Cancelled |
| 4 | Payment Required |

#### Guest Details

| **Property** | **Description** |
| --- | --- |
| contactId | The identifier for the contact if known |
| fullName | Name of guest |
| email | Email address of guest |
| attended | If the contact has attended the event |
| attendedDateTime | When the contact attended the event |

### Invoice Details

| **Property** | **Description** |
| --- | --- |
| id | The unique identifier for the invoice |
| reference | The reference number of the invoice |
| title | The title of the invoice |
| currentStatus | The current status of the invoice. The value of this field will be [one of the following current status](get-contact.md#invoice-current-status). |
| description | The description of the invoice |
| currency | The currency of the values of this invoice |
| totalCost | The total amount of the invoice |
| totalPaid | How much has been paid off the invoice |
| invoiceUrl | The URL for the invoice |
| invoiceUrlPdf | The URL for the invoice pdf |

#### Invoice current status

| **\#** | **Description** |
| --- | --- |
| 0 | Not Paid |
| 1 | Unconfirmed Paid |
| 2 | Written Off |
| 3 | Failed |
| 4 | Cancelled |
| 5 | Refunded |

The result from this call will be a [collection](../interpreting-the-response/collections.md) of all the events the user has access to. This call also accepts the [pagination](../interpreting-the-response/pagination.md) and [filter](../interpreting-the-response/filtering.md) properties.

## Throws

| **Code** | **Description** |
| --- | --- |
| Specific Code: 24096 | Unable to find contact |

The contact identifier must be provided to fetch a specific contact from the system.

