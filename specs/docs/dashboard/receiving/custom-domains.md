> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Custom Receiving Domains

> Receive emails using your own domain.

In addition to [using Resend-managed domains](/docs/dashboard/receiving/introduction#quickstart), you can also receive emails using your own custom domain.

## Enabling receiving for a new domain

Receiving emails requires an extra [MX record](/docs/knowledge-base/how-do-i-avoid-conflicting-with-my-mx-records) to work. You'll need to add this record to your DNS provider.

<Steps>
  <Step title="Verify your domain">
    If you have not already done so, [add and verify your
    domain](/docs/add-a-domain).
  </Step>

  <Step title="Navigate to the Domains page in your Dashboard" />

  <Step title="Copy the MX record" />

  <Step title="Paste the MX record into your domain's DNS service">
    <img alt="Add DNS records for Receiving Emails" src="https://mintcdn.com/resend/1QlhxulUFE6jxYM_/images/inbound-custom-domain-dns.jpg?fit=max&auto=format&n=1QlhxulUFE6jxYM_&q=85&s=0bb3258dbd1e9fc5efeb9ead53b219a2" width="2020" height="1252" data-path="images/inbound-custom-domain-dns.jpg" />
  </Step>
</Steps>

<Warning>
  If you already have existing MX records for your domain (because you're already
  using it for a real inbox, for example), we recommend that you
  create a subdomain (e.g. `subdomain.example.com`) and add the MX record
  there. This way, you can use Resend for receiving emails without affecting
  your existing email service. Note that you will *not* receive emails at Resend
  if the required `MX` record is not the lowest priority value for the domain.

  Alternatively, you can configure your email service to forward emails to an address
  that's configured in Resend or forward them directly to the SMTP server address
  that appears in the receiving `MX` record.
</Warning>

You can now [create a webhook to receive emails](/docs/dashboard/receiving/create-receiving-webhook) at your custom domain in your application.

## Enabling receiving for an existing domain

If you already have a verified domain, you can enable receiving by using the toggle in the receiving section of the domain details page.

<img alt="Enable Receiving Emails for a verified domain" src="https://mintcdn.com/resend/cxinN79qDVOa7Vo6/images/inbound-enable-receiving.jpg?fit=max&auto=format&n=cxinN79qDVOa7Vo6&q=85&s=43ea9fce84b46236ce4d58efc6004a24" width="1982" height="1232" data-path="images/inbound-enable-receiving.jpg" />

After enabling receiving, you'll see a modal showing the MX record that you need to add to your DNS provider to start receiving emails.

Once you add the MX record, confirm by clicking the **I've added the record** button and wait for the receiving record to show as "verified".

## FAQ

<AccordionGroup>
  <Accordion title="What happens if I already have MX records for my domain?">
    If you already have existing MX records for your domain, we recommend that you
    create a subdomain (e.g. `subdomain.example.com`) and add the MX record
    there.

    That's because emails will usually only be delivered to the MX record with the lowest
    priority value. Therefore, if you add Resend's MX record to your root domain alongside existing MX records,
    it will either not receive any emails at all (if the existing MX records have a lower priority),
    or it will interfere with your existing email service (if Resend's MX record has a lower priority). If you
    use the same priority, email delivery will be unpredictable and may hit either Resend or your existing email
    service.

    If you still want to use the same domain both in for Resend and your day-to-day
    email service, you can also set up forwarding rules in your existing email service
    to forward emails to an address that's configured in Resend or forward them directly
    to the SMTP server address that appears in the receiving `MX` record.
  </Accordion>

  <Accordion title="I have already verified my domain for sending. Do I need to verify it again for receiving?">
    No, you do not need to verify your entire domain again. If you already have a
    verified domain for sending, you can simply enable receiving for that domain,
    add the required MX record to your DNS provider, and click "I've added the record"
    to start verifying *only* the MX record.
  </Accordion>
</AccordionGroup>
