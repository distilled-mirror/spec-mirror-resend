> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# suppression.added

> Received when an email address is added to your suppression list.

Event triggered whenever an **email address is added to your suppression
list**. Addresses are added automatically after a hard bounce or spam
complaint, or manually through the dashboard or API.

## Response Body Parameters

All webhook payloads follow a consistent top-level structure with
event-specific data nested within the `data` object.

**type** `string`

The event type that triggered the webhook (e.g., `suppression.added`).
**created\_at** `string`

ISO 8601 timestamp when the webhook event was created.
**data** `object`

Event-specific data containing detailed information about the event. The
data object for the `suppression.added` event contains the following
parameters:

**object parameters**

**id** `string`

Unique identifier for the suppression

**email** `string`

The suppressed email address

**origin** `string`

How the address was suppressed: `bounce`, `complaint`, or `manual`

**source\_id** `string | null`

ID of the email that triggered the suppression. For suppressions with a
`manual` origin, `source_id` is `null`

**created\_at** `string`

ISO 8601 timestamp when the suppression was created

```json theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "type": "suppression.added",
  "created_at": "2026-11-17T19:32:22.980Z",
  "data": {
    "id": "e169aa45-1ecf-4183-9955-b1499d5701d3",
    "email": "steve.wozniak@gmail.com",
    "origin": "bounce",
    "source_id": "4ef9a417-02e9-4d39-ad75-9611e0fcc33c",
    "created_at": "2026-11-17T19:32:22.980Z"
  }
}
```
