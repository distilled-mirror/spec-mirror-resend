> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Partner Program Code Redemption

> Issue unique redemption codes for approved partner programs.

Issue unique, single-use promotion codes programmatically for your community members.

> [!WARNING]
>
> This endpoint is for program administrators only. Anyone with your API key can
> generate codes for your program. Do not share this endpoint or your API key
> with end users attempting to redeem codes.

## Headers

**Authorization** `string` *required*

Bearer token with your API key

**Idempotency-Key** `string` *required*

Unique identifier for each recipient request (e.g., a UUID). Reuse it only
when retrying the same request.

**Content-Type** `string` *required*

Must be `application/json`

## Body Parameters

**program\_id** `string` *required*

Your program identifier (provided by Resend)

**email** `string` *required*

Verified email address of the subscriber requesting the code

**company\_name** `string` *required*

Subscriber's company name

## Request Example

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X POST 'https://startups.resend.tools/api/v1/grants' \
  -H 'Authorization: Bearer <your_api_key>' \
  -H 'Idempotency-Key: <unique_uuid>' \
  -H 'Content-Type: application/json' \
  -d '{
    "program_id": "<your_program_id>",
    "email": "founder@startup.com",
    "company_name": "Startup Inc"
  }'
```

## Response

Every response has a `status` of `issued`, `pending_review`, or `denied`.

### Success Response

When a code is issued:

```json theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "status": "issued",
  "code": "partner-abc123xyz",
  "expires_at": "2027-02-17T00:00:00Z"
}
```

**status** `string`

Returns `issued` when a code is issued.

**code** `string`

Unique redemption code, prefixed with your partner slug (for example,
`partner-abc123xyz`).

**expires\_at** `string`

Expiration timestamp in ISO 8601 format. Varies by program.

### Pending Review Response

If your program requires manual approval, the request is queued for review and
no code is returned yet:

```json theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "status": "pending_review"
}
```

### Denied Response

When a code cannot be issued:

```json theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "status": "denied",
  "reason": "paying_customer"
}
```

**status** `string`

Returns `denied` when the code cannot be issued.

**reason** `string`

Reason the code was denied. See the table below.

| Reason | HTTP status | Meaning |
| - | - | - |
| `paying_customer` | 200 | The email belongs to an existing paid Resend account |
| `other_program` | 200 | The email already has a code from another program |
| `lifetime_cap` | 200 | Your program reached its maximum number of codes |
| `annual_plan` | 200 | The email is on an annual plan and needs manual review |
| `inactive` | 200 | Your partner account is not active |
| `resend_review` | 200 | Resend denied the request during review |
| `invalid_body` | 400 | The request body is malformed or missing required fields |
| `unknown_program` | 404 | The `program_id` does not exist |
| `unauthorized` | 401 | The API key is invalid or the `Idempotency-Key` is missing |

## Error Response

An invalid API key or a missing `Idempotency-Key` header returns `401`:

```json theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "status": "denied",
  "reason": "unauthorized"
}
```

## Code Details

* **Benefit**: Varies by program (tier and duration configured per partner)
* **Usage**: Single-use only, valid on the recipient's first purchase
* **Expiration**: Configured per program
* **Credit card**: Required at checkout when upgrading (not charged during the promotional period)

## Idempotency

This endpoint is idempotent in two ways:

* **Email-based**: Requesting a code for the same email in the same program returns the existing code.
* **Key-based**: A request with an `Idempotency-Key` that was already used returns the original response, even if the body is different.

> [!WARNING]
>
> Use a new `Idempotency-Key` for every recipient. If you reuse a key for a
> different email, you get the first recipient's code back. Reuse a key only
> when retrying the same request after a network error.

## How Recipients Redeem

1. Sign up at [resend.com](https://resend.com)
2. Go to Settings > Billing
3. Upgrade to the tier configured for your partner program
4. At checkout, enter the promotion code and add a credit card (billing starts after the promotional period ends)

## Code Revocation

If you need to revoke codes for specific users, send us their email addresses. Each code is unique and can be disabled individually.
