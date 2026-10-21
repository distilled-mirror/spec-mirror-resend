> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails with SMTP

> Learn how to integrate Resend via SMTP.

## Prerequisites

Before you start, you'll need:

* A Resend [API key](/docs/create-an-api-key)
* A [verified domain](/docs/add-a-domain)

Prefer watching a video? Check out our video walkthrough below.

[YouTube video player](https://www.youtube.com/embed/MM1JE6-inmc)

## SMTP Settings

When configuring your SMTP integration, use the following settings:

* **Host**: `smtp.resend.com`
* **Port**: `25`, `465`, `587`, `2465`, or `2587`
* **Username**: `resend`
* **Password**: `YOUR_API_KEY`

Ports help to instruct the type of security you want to use in your SMTP connection.

| Type | Port | Security |
| - | - | - |
| SMTPS | `465`, `2465` | Implicit SSL/TLS (Immediately connects via SSL/TLS) |
| STARTTLS | `25`, `587`, `2587` | Explicit SSL/TLS (First connects via plaintext, then upgrades to SSL/TLS) |

## Idempotency Key

Idempotency keys are used to prevent duplicate emails. You can add the `Resend-Idempotency-Key` header to your emails sent with SMTP to prevent duplicate emails.

```yaml SMTP {4} theme={"theme":{"light":"github-light","dark":"vesper"}}
From: Acme <onboarding@resend.dev>
To: delivered@resend.dev
Subject: hello world
Resend-Idempotency-Key: welcome-user/123456789

<p>it works!</p>
```

Learn more about [idempotency keys](/docs/dashboard/emails/idempotency-keys).

## Custom Headers

If your SMTP client supports it, you can add custom headers to your emails.

Here are some common use cases for custom headers:

* Prevent threading on Gmail with the `X-Entity-Ref-ID` header
* Include a shortcut for users to unsubscribe with the `List-Unsubscribe` header

## FAQ

Once configured, you can start sending emails via SMTP. Below are some frequently asked questions:

> **What if I need logs from the server to debug?**
>
> We currently don't provide SMTP server logs for debugging. If you run into
> issues, please [reach out to support](https://resend.com/help).

> **Where do I see the emails sent with SMTP?**
>
> Emails sent with SMTP will show in your [emails
> table](https://resend.com/emails).

> **Does the rate limit apply when sending with SMTP?**
>
> Yes, the rate limit is the [same as the
> API](https://resend.com/docs/api-reference/introduction#rate-limit).
