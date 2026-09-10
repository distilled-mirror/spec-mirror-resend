> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Which sending feature do you need?

> How to pick between our different sending features depending on your number of recipients and the nature of the message.

Resend allows you to send both **Transactional** and **Marketing** emails.

## The difference between Transactional and Marketing emails

### Transactional emails

A **Transactional email** is a message triggered by a user action or required for legal compliance. These emails are essential communications that users **cannot unsubscribe** from. Common examples include:

* Order confirmations
* Password reset emails
* Account notifications

Typically, transactional emails are **1-to-1** messages sent in response to a specific event.

### Marketing emails

A **Marketing email** is any email that is not transactional. These can be **promotional**, **informative**, or **general communication** messages.

Marketing emails are regulated by laws like **CAN-SPAM** (US) and **CASL** (Canada), and **recipients must have the option to unsubscribe**.

Examples of marketing emails:

* Promotional offers and discounts
* Newsletters
* Product updates

Marketing emails can be **1-to-1** (e.g., abandoned cart reminders) or **1-to-many** (e.g., newsletters).

## Transactional vs Marketing: Which to Choose

While not exhaustive, here's a table listing different examples of emails and the most appropriate type for each example.

| Type of Message    | Type of Recipient | Transactional | Marketing |
| ------------------ | ----------------- | ------------- | --------- |
| Order confirmation | Single            | ✓             | ⨯         |
| Password reset     | Single            | ✓             | ⨯         |
| Abandoned cart     | Single            | ⨯             | ✓         |
| Newsletter         | Multiple          | ⨯             | ✓         |
| Promotional offer  | Multiple          | ⨯             | ✓         |

## How to send an email with Resend

### How to send a Transactional email

You can send a Transactional email using:

* Our [Send Email API](/docs/api-reference/emails/send-email)
* Our [Batch Send API](/docs/api-reference/emails/send-batch-emails) (send up to 100 transactional emails in one API call)

### How to send a Marketing email

You can send Marketing emails using:

* [Resend no-code Editor](/docs/dashboard/broadcasts/introduction) – a collaborative interface for designing emails
* [Broadcast API](/docs/api-reference/broadcasts/create-broadcast) – for programmatic sending
