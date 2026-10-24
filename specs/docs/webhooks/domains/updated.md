> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# domain.updated

> Received when a domain is updated.

Event triggered when a **domain was successfully updated**.

> [!NOTE]
>
> If you're having issues verifying your domain, [review our guide on a domain
> not verifying](https://resend.com/docs/knowledge-base/what-if-my-domain-is-not-verifying.md) for
> troubleshooting steps.

## Response Body Parameters

All webhook payloads follow a consistent top-level structure with
event-specific data nested within the `data` object.

**type** `string`

The event type that triggered the webhook (e.g., `domain.updated`).
**created\_at** `string`

ISO 8601 timestamp when the webhook event was created.
**data** `object`

Event-specific data containing detailed information about the event. The
data object for the `domain.updated` event contains the following
parameters:

**object parameters**

**id** `string`

Unique identifier for the domain

**name** `string`

Domain name (e.g., `example.com`)

**status** `verified | partially_verified | partially_failed | failed | pending | not_started`

Current verification status of the domain:

* `verified`: The domain is verified and can be used to send or receive emails.
* `partially_verified`: One capability (send or receive) is verified while the other is still pending verification.
* `partially_failed`: The domain is verified but one of the features (send or receive) is not verified.
* `pending`: The domain is pending verification and cannot be used to send or receive emails.
* `not_started`: Verification has not started yet, so the domain cannot be used to send or receive emails.
* `failed`: The domain failed verification.

> [!NOTE]
>
> The `data.status` field represents an aggregated status of the domain. For
> domains that can both [send](https://resend.com/docs/dashboard/emails/introduction.md) and
> [receive](https://resend.com/docs/dashboard/receiving/introduction.md) emails, the status may be
> `partially_verified` (one capability verified, the other pending) or
> `partially_failed` (one capability verified, the other failed).

**created\_at** `string`

ISO 8601 timestamp when the domain was created

**region** `us-east-1 | eu-west-1 | sa-east-1 | ap-northeast-1`

AWS region where the domain is configured.

**capabilities** `object`

Domain capabilities for sending and receiving emails.

**properties**

**sending** `enabled | disabled`

Whether the domain can be used to send emails.

**receiving** `enabled | disabled`

Whether the domain can be used to receive emails.

**records** `array`

Array of DNS record objects required for domain verification

**record object**

**record** `SPF | DKIM | Receiving MX | Tracking | TrackingCAA`

Record type purpose. Learn more about [domain verification records](https://resend.com/docs/dashboard/domains/introduction.md).

**name** `string`

DNS record name/subdomain

**type** `MX | TXT | CNAME | CAA`

DNS record type

**value** `string`

DNS record value to be set

**ttl** `string`

Time to live for the DNS record

**status** `string`

Verification status of this specific record

**priority** `number`

Priority value for MX records (optional)

```json theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "type": "domain.updated",
  "created_at": "2026-11-17T19:32:22.980Z",
  "data": {
    "id": "d91cd9bd-1176-453e-8fc1-35364d380206",
    "name": "example.com",
    "status": "not_started",
    "created_at": "2026-04-26T20:21:26.347Z",
    "region": "us-east-1",
    "capabilities": {
      "sending": "enabled",
      "receiving": "enabled"
    },
    "records": [
      {
        "record": "SPF",
        "name": "send",
        "type": "MX",
        "ttl": "Auto",
        "status": "not_started",
        "value": "feedback-smtp.us-east-1.amazonses.com",
        "priority": 10
      },
      {
        "record": "SPF",
        "name": "send",
        "value": "\"v=spf1 include:amazonses.com ~all\"",
        "type": "TXT",
        "ttl": "Auto",
        "status": "not_started"
      },
      {
        "record": "DKIM",
        "name": "resend._domainkey",
        "value": "p=MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQDsc4Lh8xilsngyKEgN2S84+21gn+x6SEXtjWvPiAAmnmggr5FWG42WnqczpzQ/mNblqHz4CDwUum6LtY6SdoOlDmrhvp5khA3cd661W9FlK3yp7+jVACQElS7d9O6jv8VsBbVg4COess3gyLE5RyxqF1vYsrEXqyM8TBz1n5AGkQIDAQA2",
        "type": "TXT",
        "status": "not_started",
        "ttl": "Auto"
      },
      {
        "name": "inbound.yourdomain.tld",
        "priority": 10,
        "record": "Receiving MX",
        "status": "pending",
        "ttl": "Auto",
        "type": "MX",
        "value": "inbound-smtp.us-east-1.amazonaws.com"
      }
    ]
  }
}
```
