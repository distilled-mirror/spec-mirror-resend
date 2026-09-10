> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Why are my emails landing on the Suppression List?

> Learn why your emails land on the Suppression List and how to remove them.

When sending to an email address results in a hard bounce or spam complaint, Resend places this address on the Suppression List. Future emails to addresses on the list will be marked as `suppressed` and won't be delivered until the address is removed.

<Info>
  We place emails on the Suppression List to protect domain reputation, both
  yours and ours. Sending an email to a known hard bounce recipient can damage
  domain reputation and affect email deliverability.
</Info>

## Reasons emails are placed on the Suppression List

Here are some possible reasons an email address is placed on the Suppression List:

* The recipient's email address **contains a typo**.
* The recipient's email address **doesn't exist**.
* The recipient's email server has **permanently blocked delivery**.
* The recipient has marked a previous delivery as spam.

## What happens when you send to an address on the Suppression List

Whenever you send an email with Resend, the recipient is checked against the suppression list. If they're on it, the delivery is [suppressed](/docs/dashboard/emails/email-suppressions) to prevent damaging your sender reputation and our infrastructure.

Suppressed emails will appear with a `suppressed` status in your [Emails](https://resend.com/emails) dashboard:

<img src="https://mintcdn.com/resend/Nyu32IXsxRkmP92c/images/email-suppression-visibility-1.png?fit=max&auto=format&n=Nyu32IXsxRkmP92c&q=85&s=a40d291604cd8ddcc40f962e0b488da6" alt="Email Suppression in Dashboard" class="extraWidth" width="1778" height="1088" data-path="images/email-suppression-visibility-1.png" />

## View suppression details

You can view the reason an email was suppressed on the [Emails](https://resend.com/emails) page:

1. Open the [Emails](https://resend.com/emails) page and search for the recipient's email address in question.
2. Click on the email to view its details.
3. The suppression details will show suggested fixes to help you resolve the issue.

<video src="https://mintcdn.com/resend/pSrJMzMw3NZ5HeOx/images/email-suppression-visibility-2.mp4?fit=max&auto=format&n=pSrJMzMw3NZ5HeOx&q=85&s=381c6bd7a7b056dc760266f2d3b69afe" autoPlay loop muted playsInline class="extraWidth" data-path="images/email-suppression-visibility-2.mp4" />

## Removing an email address from the Suppression List

You may be able to send a message to the same recipient in the future if the issue that caused the original bounce or complaint is resolved and the email address is removed from the Suppression List.

<Warning>
  Remember, if you do not address the issue that caused the email to bounce, the
  email address will return to the Suppression List the next time you attempt to
  send to it.
</Warning>

To remove your recipient from the Suppression List, click on the suppressed email in the [emails dashboard](https://resend.com/emails), and click **Remove from suppression list**.
