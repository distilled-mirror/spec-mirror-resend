> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# How to avoid conflicts with your MX records

> Learn how to avoid conflicts with your existing MX records when setting up a Resend domain.

## MX records for sending and receiving emails

MX (Mail Exchanger) records specify where incoming mail is delivered on behalf of a domain. Every MX value has a unique priority (also known as preference) value. The lower the number, the higher the priority.

Resend may require that you setup a MX record on two occasions:

1. **[Enabling your domain to send emails](https://resend.com/docs/dashboard/emails/introduction)**: You need to setup an MX record on `send.example.com` to establish a return-path for bounce/complaint reports from Inbox Providers. This return path is set in the email headers of every email you send through Resend.

<Info>
  For domains created after August 2026, Resend may generate CNAME records for sending instead of the MX and TXT pair, in which case this occasion doesn't apply to your domain. Always add the exact records shown in your domain's **Records** tab within the Resend dashboard.

  Note that a CNAME record cannot co-exist with any other record on the same subdomain, so if you already have other records set for `send.example.com`, you will need to either configure a different `Return-Path` subdomain (e.g. `bounce.example.com`) or remove the existing records for `send.example.com`.
</Info>

2. **[Enabling your domain to receive emails](https://resend.com/docs/dashboard/receiving/custom-domains)**: You can setup an MX record on your domain to route all received emails to Resend.

## Avoiding conflicts with MX record priorities

Here's an example for each occasion Resend requires you to setup a MX record.

Say you're using G Suite for your email. You'll have an MX record that looks something like this:

```
example.com     MX    10 alt3.aspmx.l.google.com.
```

This record specifies that any incoming mail to `<anything>@example.com` is delivered to the Google servers.

Now, say you want to use Resend to send emails from `@example.com`. You'll need to add an MX record for `send.example.com` that looks something like this:

```
send.example.com     MX    10 feedback-smtp.us-east-1.amazonses.com
```

This **won't** conflict because the MX record is for `send.example.com`, not `example.com`. MX records only impact the subdomain they are associated to, so the Resend MX record will not affect your existing records on the root domain.

Now say you want to start receiving emails through Resend.

Because you already have the MX record `example.com`, you have two options:

1. **\[Recommended] Create a MX record for a subdomain** (e.g. `subdomain.example.com`). Now emails sent to `<anything>@example.com` will continue going to G Suite, and emails sent to `<anything>@subdomain.domain.com` will go to Resend.

2. **Create a MX record with the lowest priority** among the other MX record for your domain.
   Since on our example, you already had a MX record for `example.com` point to G Suite, you would create:

```
example.com    MX    9  inbound-smtp.us-east-1.amazonaws.com
```

Now this MX record priority has a lower value (higher priority) so it will be prioritized. But keep in mind that:

<Note>
  * This will route all emails destined to `<anything>@example.com` to Resend, instead of your previous provider (e.g., G Suite).
  * If two MX records have the same priority value, this does not mean it will send to both servers. Instead, only one server will be chosen, randomly, per email delivery attempt.
</Note>

## Solving common conflicts

<AccordionGroup>
  <Accordion title="Conflicts with existing records">
    If you already have a MX record set for `send.example.com`, you will need to remove it before adding the Resend MX record.

    If you need to keep the existing record, you can add a subdomain to your domain (e.g. `sub.example.com`) which will move the Resend MX location to `send.sub.example.com`.
  </Accordion>

  <Accordion title="Conflicts with existing priority">
    Each MX should have a unique priority value. We suggest using 10 for your MX record on `send.example.com`, but you can use a lower number (higher priority) if 10 is already in use.

    <Note>
      The lowest possible value (highest priority) is 0. So if you already have a record with this priority, you'll need to remove it in order to create the MX record for Resend.
    </Note>
  </Accordion>
</AccordionGroup>
