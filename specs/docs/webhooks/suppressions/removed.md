> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# suppression.removed

> Received when an email address is removed from your suppression list.

Event triggered whenever an **email address is removed from your suppression
list**.

## Response Body Parameters

All webhook payloads follow a consistent top-level structure with
event-specific data nested within the `data` object.

**type** `string`

The event type that triggered the webhook (e.g., `suppression.removed`).
**created\_at** `string`

ISO 8601 timestamp when the webhook event was created.
**data** `object`

Event-specific data containing detailed information about the event. The
data object for the `suppression.removed` event contains the following
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
  "type": "suppression.removed",
  "created_at": "2026-11-17T19:32:22.980Z",
  "data": {
    "id": "e169aa45-1ecf-4183-9955-b1499d5701d3",
    "email": "steve.wozniak@gmail.com",
    "origin": "manual",
    "source_id": null,
    "created_at": "2026-11-15T08:12:45.120Z"
  }
}
```
