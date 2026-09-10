> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Email Bounces

> Understanding and resolving delivery issues.

## Why emails bounce

A bounce happens when an email cannot be delivered to the person it was meant for, and is returned to the sender. It essentially "bounces" back to the person who sent it.

Some reasons include invalid email addresses, full mailboxes, and technical issues with email servers. Other causes are spam filters, message size restrictions, or blacklisting of the sender's email server.

## Bounce Types and Subtypes

When an email bounces, Resend receives a message from the recipient's mail server. The bounce message explains why the delivery failed so the sender can fix the issue.

There are three types of bounces:

1. `Permanent` - also known as "hard bounce,” where the recipient's mail server rejects the email and will never be delivered.
   * `General` - The recipient's email provider sent a hard bounce message.
   * `NoEmail` - It was not possible to retrieve the recipient email address from the bounce message.

2. `Transient` - also known as "soft bounce,” where the recipient's mail server rejects the email but it may be delivered in the future.
   * `General` - The recipient's email provider sent a general bounce message. You might be able to send a message to the same recipient in the future if the issue that caused the message to bounce is resolved.
   * `MailboxFull` - The recipient's email provider sent a bounce message because the recipient's inbox was full. You might be able to send to the same recipient in the future when the mailbox is no longer full.
   * `MessageTooLarge` - The recipient's email provider sent a bounce message because message you sent was too large. You might be able to send a message to the same recipient if you reduce the size of the message.
   * `ContentRejected` - The recipient's email provider sent a bounce message because the message you sent contains content that the provider doesn't allow. You might be able to send a message to the same recipient if you change the content of the message.
   * `AttachmentRejected` - The recipient's email provider sent a bounce message because the message contained an unacceptable attachment. For example, some email providers may reject messages with attachments of a certain file type, or messages with large attachments. You might be able to send a message to the same recipient if you remove or change the content of the attachment.

<Tip>
  Sometimes, inboxes use autoresponders to signal a bounce. A `transient` status
  could mean it's related to the autoresponder, and it's not a permanent issue.
</Tip>

3. `Undetermined` - where the recipient's email server bounced, but the bounce message didn't contain enough information for Resend to determine the underlying reason.
   * `Undetermined` - The recipient's email provider sent a bounce message. The bounce message didn't contain enough information for Resend to determine the reason for the bounce.

## Viewing Bounce Details in Resend

You can see the bounce details by clicking on the email, and hovering over the `Bounced` label.

<img alt="Email Bounce Notification" src="https://mintcdn.com/resend/OWNnQaVDyqcGyhhN/images/email-bounce-details-1.png?fit=max&auto=format&n=OWNnQaVDyqcGyhhN&q=85&s=f0f99293137b8de4a9862b05cfd87d74" width="3024" height="1888" data-path="images/email-bounce-details-1.png" />

Once you click **See Details**, the drawer will open on the right side of your screen with the bounce type, subtype, along with suggestions on how to proceed.

If the email is on the suppression list, you can click **Remove from Suppression List** to remove it.

<img alt="Email Bounce Drawer" src="https://mintcdn.com/resend/OWNnQaVDyqcGyhhN/images/email-suppression-list-2.png?fit=max&auto=format&n=OWNnQaVDyqcGyhhN&q=85&s=baf9f0a40313b856be978b728fb1d01c" width="2992" height="1868" data-path="images/email-suppression-list-2.png" />
