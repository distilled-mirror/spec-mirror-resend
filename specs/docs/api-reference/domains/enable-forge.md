> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Enable Forge

> Put a domain's sending on Resend Forge.

This endpoint returns the DNS record Forge needs. Add it to your DNS and call
[Verify Domain](https://resend.com/docs/api-reference/domains/verify-domain.md) with `scope: ["forge"]`,
then poll [Retrieve Domain](https://resend.com/docs/api-reference/domains/get-domain.md) until the
Forge record's `status` is `verified`.
Calling this endpoint again just returns the current state.

> [!NOTE]
>
> The domain keeps sending through its current records while the Forge record
> verifies, so there is no interruption.

> [!NOTE]
>
> The domain must be a sending domain. Receive-only domains, domains on a
> dedicated IP, and domains with legacy DKIM get a `forge_unavailable` error.

## Path Parameters

The Domain ID.

## Body Parameters

The subdomain label for the Forge return path, for example `forge` on
`example.com` produces a `CNAME` record for `forge.example.com`. It must start
with a letter, end with a letter or digit, contain only letters, digits, and
hyphens, and be 63 characters or less. It is stored lowercased. When omitted,
Resend picks a label that is free in your DNS. It cannot equal the domain's
current return path, and the chosen host must not already have DNS records;
either case gets a `return_path_unavailable` error. It is set once and cannot
be changed afterwards.

## Headers

**Idempotency-Key** `string`

Add an idempotency key to enable Forge only once.

* Should be **unique per API request**
* Idempotency keys expire after **24 hours**
* Have a maximum length of **256 characters**
* A retry with the same key returns the first successful response, with the
  `idempotent-replayed: true` header
* A failed request is not stored, so you can retry it with the same key
* Reusing the key with a different body, or while the first request is still
  running, returns a `409`

[Learn more](https://resend.com/docs/dashboard/emails/idempotency-keys.md)

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.domains.forge.enable({
  id: 'd91cd9bd-1176-453e-8fc1-35364d380206',
  customReturnPath: 'forge',
});
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X POST 'https://api.resend.com/domains/d91cd9bd-1176-453e-8fc1-35364d380206/forge' \
     -H 'Authorization: Bearer re_xxxxxxxxx' \
     -H 'Content-Type: application/json' \
     -d '{"custom_return_path": "forge"}'
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "domain",
  "id": "d91cd9bd-1176-453e-8fc1-35364d380206",
  "name": "example.com",
  "created_at": "2023-04-26T20:21:26.347412+00:00",
  "status": "partially_verified",
  "capabilities": {
    "sending": "enabled",
    "receiving": "disabled"
  },
  "records": [
    {
      "record": "DKIM",
      "name": "resend._domainkey",
      "value": "p=MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQC...",
      "type": "TXT",
      "status": "verified",
      "ttl": "Auto"
    },
    {
      "record": "SPF",
      "name": "send",
      "type": "MX",
      "ttl": "Auto",
      "status": "verified",
      "value": "feedback-smtp.us-east-1.amazonses.com",
      "priority": 10
    },
    {
      "record": "SPF",
      "name": "send",
      "value": "v=spf1 include:amazonses.com ~all",
      "type": "TXT",
      "ttl": "Auto",
      "status": "verified"
    },
    {
      "record": "SPF",
      "name": "forge",
      "value": "send.forge.rmta.net",
      "type": "CNAME",
      "status": "pending",
      "ttl": "Auto"
    }
  ],
  "region": "us-east-1",
  "open_tracking": false,
  "click_tracking": false
}
```
