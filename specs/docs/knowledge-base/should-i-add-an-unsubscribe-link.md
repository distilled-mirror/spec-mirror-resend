> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Do you need to add an unsubscribe link to all of your emails sent with Resend?

> Learn best practices about using unsubscribe links.

Transactional emails are generally exempt from including an unsubscribe link. Unlike marketing emails, transactional emails serve a functional purpose, such as account confirmation, password resets, and order confirmations.

As a best practice, tell recipients how to opt out of receiving future email from you if the content is more related to nurturing relationships with your customers, rather than pragmatic, action-oriented emails.

Laws enforced by the FTC and GDPR prioritize giving recipients a clear way to give and withdraw their consent to receiving email marketing content. Additionally, not having an option for opting out of emails risks recipients complaining or marking the email as spam, which can hurt your reputation as a sender.

Here is more on how to [manually add and manage unsubscribe links](https://resend.com/docs/dashboard/emails/add-unsubscribe-to-transactional-emails).

If you're using [Resend Broadcasts or Automations](https://resend.com/docs/dashboard/audiences/managing-unsubscribe-list), Resend will automatically handle unsubscribe requests once you include `{{{RESEND_UNSUBSCRIBE_URL}}}` in your email. You can include the Unsubscribe Footer in your Broadcasts, which will be automatically replaced with the correct link for each contact, or use `{{{RESEND_UNSUBSCRIBE_URL}}}` as a link target if you want to customize the unsubscribe footer.
