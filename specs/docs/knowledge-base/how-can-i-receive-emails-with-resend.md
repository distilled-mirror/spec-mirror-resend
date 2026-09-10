> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Can You Receive Emails with Resend?

> Receive emails with webhooks and process content, attachments, forwarding, and replies.

Yes. Resend supports receiving emails (inbound) via webhooks.

With Receiving, you can:

* Receive incoming emails and get notified with the `email.received` webhook event.
* Retrieve full email content (HTML, text, headers) using the Receiving API.
* Process attachments using attachment metadata and temporary download URLs.

You can receive emails at:

* A Resend-managed `*.resend.app` receiving domain, or
* Your own custom domain by adding the required `MX` record.

See the full guide: [Receiving Emails](/docs/dashboard/receiving/introduction).
