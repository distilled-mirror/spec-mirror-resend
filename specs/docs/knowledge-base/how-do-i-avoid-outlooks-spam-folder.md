> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# How to avoid Outlook's spam folder

> Learn how to improve inbox placement in Outlook.

<Note>
  This guide is adapted from Microsoft's article to [Improve your spam
  reputation](https://support.microsoft.com/en-us/office/sender-support-in-outlook-com-05875e8d-1950-4d89-a5c3-adc355d0d652).
  For high-volume senders (5,000+ messages per day), see [Microsoft's bulk
  sending requirements for
  2025](https://resend.com/blog/microsoft-bulk-sending-requirements-2025).
</Note>

* **Set up email authentication**. Configure [SPF, DKIM, and DMARC](/docs/dashboard/domains/introduction) for your domain. This is required for bulk senders (5,000+ messages per day) and strongly recommended for all senders.

* **Add your sender name**. Set your `from` like this: `"Name <name.domain.com>"`.

* **Engage with your own email**. Send an email to yourself, open it, and reply to it.

* **Add yourself as a contact**. See how to add contacts in [Outlook.com](https://support.microsoft.com/en-us/office/create-view-and-edit-contacts-and-contact-lists-in-outlook-com-5b909158-036e-4820-92f7-2a27f57b9f01).

* **Ask your recipients to add you in their contacts**. This can be done in [Outlook](https://support.microsoft.com/en-us/office/add-recipients-of-my-email-messages-to-the-safe-senders-list-be1baea0-beab-4a30-b968-9004332336ce) or [outlook.com](https://support.microsoft.com/en-us/office/safe-senders-in-outlook-com-470d4ee6-e3b6-402b-8cd9-a6f00eda7339).

* **Don't blast to a BCC list**. Send separate emails if you are sending to a large number of recipients.

* **Prevent over sending**. Limits are impacted by historical engagements and sending volumes, so avoid sending too many emails at once. If you think this is an issue, reduce the frequency or volume.

* **Send to engaged recipients**. Don't keep sending if there is no engagement from your recipients. This is especially true if a recipient has requested to unsubscribe or an address is bouncing. Keep spam complaint rates under 0.3%.

* **Include an unsubscribe option**. For bulk emails, include a clearly visible unsubscribe link. Consider implementing [one-click unsubscribe](/docs/dashboard/emails/add-unsubscribe-to-transactional-emails) for the best user experience.

* **Limit use of HTML**. Keep emails as close to plain text as possible.
