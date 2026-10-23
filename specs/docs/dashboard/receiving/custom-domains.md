> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Custom Receiving Domains

> Receive emails using your own domain.

In addition to [using Resend-managed domains](/docs/dashboard/receiving/introduction.md#quickstart), you can also receive emails using your own custom domain.

## Enabling receiving for a new domain

Receiving emails requires an extra [MX record](/docs/knowledge-base/how-do-i-avoid-conflicting-with-my-mx-records.md) to work. You'll need to add this record to your DNS provider.

**1. Verify your domain**

If you have not already done so, [add and verify your
domain](/docs/add-a-domain.md).

**2. Navigate to the Domains page in your Dashboard**

**3. Copy the MX record**

**4. Paste the MX record into your domain's DNS service**

![Add DNS records for Receiving Emails](https://mintcdn.com/resend/1QlhxulUFE6jxYM_/images/inbound-custom-domain-dns.jpg?fit=max\&auto=format\&n=1QlhxulUFE6jxYM_\&q=85\&s=0bb3258dbd1e9fc5efeb9ead53b219a2)

> [!WARNING]
>
> If you already have existing MX records for your domain (because you're already
> using it for a real inbox, for example), we recommend that you
> create a subdomain (e.g. `subdomain.example.com`) and add the MX record
> there. This way, you can use Resend for receiving emails without affecting
> your existing email service. Note that you will *not* receive emails at Resend
> if the required `MX` record is not the lowest priority value for the domain.
>
> Alternatively, you can configure your email service to forward emails to an address
> on a domain where receiving is verified in Resend. Don't forward directly to the
> SMTP server address that appears in the receiving `MX` record: Resend drops emails
> for domains whose receiving `MX` record isn't verified.

You can now [create a webhook to receive emails](/docs/dashboard/receiving/create-receiving-webhook.md) at your custom domain in your application.

## Enabling receiving for an existing domain

If you already have a verified domain, you can enable receiving by using the toggle in the receiving section of the domain details page.

![Enable Receiving Emails for a verified domain](https://mintcdn.com/resend/cxinN79qDVOa7Vo6/images/inbound-enable-receiving.jpg?fit=max\&auto=format\&n=cxinN79qDVOa7Vo6\&q=85\&s=43ea9fce84b46236ce4d58efc6004a24)

After enabling receiving, you'll see a modal showing the MX record that you need to add to your DNS provider to start receiving emails.

> [!NOTE]
>
> Always copy the MX record value shown on your domain's page in Resend. The
> values in this guide are examples. Depending on your domain you will see
> `receive.forge.rmta.net`, a regional variant such as
> `receive-euw1.forge.rmta.net`, or `inbound-smtp.<region>.amazonaws.com`.

Once you add the MX record, confirm by clicking the **I've added the record** button and wait for the receiving record to show as "verified".

## FAQ

> **What happens if I already have MX records for my domain?**
>
> If you already have existing MX records for your domain, we recommend that you
> create a subdomain (e.g. `subdomain.example.com`) and add the MX record
> there.
>
> That's because emails will usually only be delivered to the MX record with the lowest
> priority value. Therefore, if you add Resend's MX record to your root domain alongside existing MX records,
> it will either not receive any emails at all (if the existing MX records have a lower priority),
> or it will interfere with your existing email service (if Resend's MX record has a lower priority). If you
> use the same priority, email delivery will be unpredictable and may hit either Resend or your existing email
> service.
>
> If you still want to use the same domain both in for Resend and your day-to-day
> email service, you can also set up forwarding rules in your existing email service
> to forward emails to an address on a domain where receiving is verified in Resend.
> Forwarding directly to the SMTP server address that appears in the receiving `MX`
> record doesn't work: Resend drops emails for domains whose receiving `MX` record
> isn't verified.

> **I have already verified my domain for sending. Do I need to verify it again for receiving?**
>
> No, you do not need to verify your entire domain again. If you already have a
> verified domain for sending, you can simply enable receiving for that domain,
> add the required MX record to your DNS provider, and click "I've added the record"
> to start verifying *only* the MX record.

> **I want my domain to only receive emails, not send emails from Resend. Is that possible?**
>
> Yes, on the domain details page, turn off "Enable Sending". You no longer need Resend's SPF records, so you can remove them from your DNS host. You still need our DKIM record to stay published, and the receiving `MX` record with "Enable Receiving" turned on.
